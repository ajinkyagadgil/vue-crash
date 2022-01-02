<template>
  <div v-if="showAddTask">
    <AddTask @add-task="addTask" />
  </div>
  <Tasks :tasks="tasks" @delete-task="deleteTask" @task-toggle="toggleTask" />
</template>

<script>
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";
export default {
  name: 'Home',
  components: {Tasks, AddTask},
  data() {
    return {
      tasks: []
    };
  },
  props: {
    showAddTask: Boolean,
  },
    methods: {
    async deleteTask(id) {
      if (confirm("Are you sure you want to delete")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });

        if (res.status === 200) {
          this.tasks = this.tasks.filter((task) => task.id !== id);
        } else {
          alert("Error in deleting the data");
        }
      }
    },
    async addTask(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });

      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },
    async toggleTask(id) {
      const taskToToggle = await this.fetchTask(id);
      const updTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updTask),
      });

      const data = await res.json();
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    async fetchTasks() {
      const res = await fetch("/api/tasks");
      return await res.json();
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      return await res.json();
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>