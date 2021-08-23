<template>
  <div>
    <ListItem v-for="todoObj in todos" :key="todoObj.id" :todo="todoObj" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
  </div>
</template>

<script>
import ListItem from "./ListItem";

export default {
  name: "List",
  components: {
    ListItem
  },
  props: ['todos', "checkTodo", "deleteTodo"]
}
</script>

<style scoped>

</style>