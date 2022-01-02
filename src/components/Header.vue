<template>
  <header>
    <h1>{{ titleName }}</h1>
    <!-- <Button @btn-click="$emit('toggle-add-task')" text="Add Task" color="green"/> -->
    <Button @btn-click="$emit('toggle-add-task')" :text="toggleAddTaskBtn ? 'Close':'Add Task'" :color="toggleAddTaskBtn ? 'red':'green'"/>
  </header>
</template>

<script>
import Button from './Button'
export default {
  name: "Header",
  //   props:['titleName']  first way to declare props

  //Below is the second way to include the props using object and use the type as well
  // props:{
  //     titleName: String
  // }

  //In this way we can add a default value so even if we do not pass anything it takes this default value
  props: {
    titleName: {
        type: String,
        default:'Hello World'
    },
    toggleAddTaskBtn: Boolean
  },
  components: {
      Button
  }
};
</script>
    
<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>