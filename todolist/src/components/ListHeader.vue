<template>
  <div class="todo-header">
    <b-form-input v-model="text" placeholder="Enter a task and press enter" @keyup.enter="add"/>
    <button class="list-header-button enter" @click="add">Enter</button>
  </div>
</template>

<script>
import {nanoid} from 'nanoid'

export default {
  name: "ListHeader",
  data() {
    return {
      text: ""
    }
  },
  methods: {
    add() {
      if(!this.text.trim()) return alert("Input cannot be empty")
      const todoObj = {id: nanoid(), title: this.text, done: false, isEdit: false}
      this.$emit('addTodo', todoObj)
      this.text = ""
    }
  }
}
</script>

<style scoped>
.todo-header {
  display: flex;
}

.list-header-button {
  color: white;
  border: none;
  padding: 0.8vh 1vw;
  border-radius: 5px;
}

.enter {
  background-color: #0275d8;
}

.enter:hover {
  background-color: #0A6CC0FF;
}
</style>