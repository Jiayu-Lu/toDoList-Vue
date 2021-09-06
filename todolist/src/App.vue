<template>
  <div id="app">
    <b-container>
      <b-row align-h="center">
        <b-col sm="10" xs="12">
          <ListHeader @addTodo="addTodo"></ListHeader>
          <ListFooter :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"></ListFooter>
          <List :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"></List>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import pubsub from 'pubsub-js';
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
      todos: JSON.parse(localStorage.getItem('todos')) || [],
      pubId: ""
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
    deleteTodo(_, id) {
      this.todos = this.todos.filter(todo => {
        return todo.id !== id
      })
    },
    checkAllTodo(done) {
      this.todos.forEach(todo => {
        todo.done = done
      })
    },
    clearAllTodo() {
      this.todos = this.todos.filter(todo => {
        return !todo.done
      })
    },
    updateTodo(_, data) {
      this.todos.forEach((todo) => {
        if(todo.id === data.todoId) {
          todo.title = data.todoTitle
        }
      })
    }
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem('todos', JSON.stringify(value))
      }
    }
  },
  mounted() {
    this.deleteTodoPubId = pubsub.subscribe('deleteTodo', this.deleteTodo)
    this.updateTodoPubId = pubsub.subscribe('updateTodo', this.updateTodo)
  },
  beforeDestroy() {
    pubsub.unsubscribe(this.deleteTodoPubId)
    pubsub.unsubscribe(this.updateTodoPubId)
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
    min-height: 100vh;
    padding: 2vh 1vw;
  }
</style>
