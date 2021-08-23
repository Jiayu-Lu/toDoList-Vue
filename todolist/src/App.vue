<template>
  <div id="app">
    <b-container>
      <b-row align-h="center">
        <b-col sm="10" xs="12">
          <ListHeader :addTodo="addTodo"></ListHeader>
          <List :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"></List>
          <ListFooter :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"></ListFooter>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import ListHeader from "./components/ListHeader";
import List from "./components/List";
import ListFooter from "./components/ListFooter";

export default {
  name: 'App',
  components: {
    ListHeader,
    List,
    ListFooter
  },
  data() {
    return {
      todos: [
        {id: '001', title: 'chouyan', done: false},
        {id: '002', title: 'hejiu', done: false},
        {id: '003', title: 'kaiche', done: false}
      ]
    }
  },
  methods: {
    addTodo(todoObj) {
      this.todos.unshift(todoObj)
    },
    checkTodo(id) {
      this.todos.forEach(todo => {
        if(todo.id === id) todo.done = !todo.done
      })
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => {
        return todo.id !== id
      })
    },
    checkAllTodo(done) {
      this.todos.forEach(todo => {
        console.log(todo, done)
        todo.done = done
      })
    },
    clearAllTodo() {
      this.todos = this.todos.filter(todo => {
        return !todo.done
      })
    }
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  #app {
    margin: 2vh auto;
  }
</style>
