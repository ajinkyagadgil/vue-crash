<template>
  <div :key="task.id" v-for="task in tasks">
    <Task :task="task" @task-toggle="$emit('task-toggle', task.id)" @delete-task="$emit('delete-task',task.id)" />
  </div>
</template>

<script>
import Task from "./Task.vue";
export default {
  name: "Tasks",
  props: {
    tasks: Array,
  },
  components: {
    Task,
  },
  emits:['delete-task', 'task-toggle']
};
</script>

<style scoped>
</style>