<template>
  <div class="todo-header">
    <b-form-input v-model="text" placeholder="Enter a task and press enter" @keyup.enter="add"/>
  </div>
</template>

<script>
import {nanoid} from 'nanoid'

export default {
  name: "ListHeader",
  props: ["addTodo"],
  data() {
    return {
      text: ""
    }
  },
  methods: {
    add() {
      if(!this.text.trim()) return alert("Input cannot be empty")
      const todoObj = {id: nanoid(), title: this.text, done: false}
      this.addTodo(todoObj)
      this.text = ""
    }
  }
}
</script>

<style scoped>
.todo-header {

}
</style>