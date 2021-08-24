<template>
  <div class="list-item">
    <b-form-checkbox
        :checked="todo.done"
        @change="handleCheck(todo.id)"
        class="list-item-text"
    >
      {{todo.title}}
    </b-form-checkbox>
    <button class="list-item-button" @click="handleDelete(todo.id)">Delete</button>
  </div>
</template>

<script>
export default {
  name: "ListItem",
  props: ['todo', "checkTodo", "deleteTodo"],
  methods: {
    handleCheck(id) {
      this.checkTodo(id)
    },
    handleDelete(id) {
      if(confirm("Are you sure you want to delete this task")) {
        this.deleteTodo(id)
      }
    }
  }
}
</script>

<style scoped>
.list-item {
  min-height: 8vh;
  padding: 1vh 1vw;
  border: 1px solid #ddd;

  display: flex;
  justify-content: space-between;
  justify-items: center;
}
.list-item:hover {
  background-color: #ddd;
}

.list-item-text {
  width: 80%;
  word-break: break-word;
}

.list-item:hover .list-item-button{
  display: block;
}

.list-item-button {
  display: none;
  background-color: #d9534f;
  color: white;
  border: none;
  padding: 0.8vh 1vw;
  border-radius: 5px;
}

.list-item-button:hover {
  background-color: #BD5A51FC;
}

</style>