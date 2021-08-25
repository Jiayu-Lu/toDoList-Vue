<template>
  <div class="list-item">
    <b-form-checkbox
        :checked="todo.done"
        @change="handleCheck(todo.id)"
        class="list-item-text"
    >
      <span v-show="!todo.isEdit">{{todo.title}}</span>
      <input v-show="todo.isEdit" type="text" :value="todo.title" @blur="handleBlur(todo, $event)" ref="inputTitle">
    </b-form-checkbox>
    <button v-show="todo.isEdit" class="list-item-button confirm" @click="handleConfirm(todo, $event)">Confirm</button>
    <button v-show="todo.isEdit" class="list-item-button cancel" @click="handleCancel(todo)">Cancel</button>
    <button v-show="!todo.isEdit" class="list-item-button edit" @click="handleEdit(todo)">Edit</button>
    <button v-show="!todo.isEdit" class="list-item-button delete" @click="handleDelete(todo.id)">Delete</button>
  </div>
</template>

<script>
import pubsub from 'pubsub-js'
export default {
  name: "ListItem",
  props: ['todo', "checkTodo", "deleteTodo"],
  methods: {
    handleCheck(id) {
      this.checkTodo(id)
    },
    handleDelete(id) {
      if(confirm("Are you sure you want to delete this task")) {
        pubsub.publish('deleteTodo', id)
      }
    },
    handleEdit(todo) {
      todo.isEdit = true
      this.$nextTick(function() {
        this.$refs.inputTitle.focus()
      })
    },
    handleBlur(todo, e) {
      this.todo.isEdit = false
      if(!e.target.value.trim()) return alert("the task cannot be empty")
      pubsub.publish('updateTodo', {todoId: todo.id, todoTitle: e.target.value})
    },
    handleConfirm(todo, e) {
      this.todo.isEdit = false
      if(!e.target.value.trim()) return alert("the task cannot be empty")
      pubsub.publish('updateTodo', {todoId: todo.id, todoTitle: e.target.value})
    },
    handleCancel(todo) {
      todo.isEdit = false
    }
  }
}
</script>

<style scoped>
.list-item {
  background-color: #f7f7f7;
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
  color: white;
  border: none;
  padding: 0.8vh 1vw;
  border-radius: 5px;
}

.confirm {
  background-color: #5cb85c;
}

.confirm:hover {
  background-color: #559F55FF;
}

.edit {
  background-color: #0275d8;
}

.edit:hover {
  background-color: #0A6CC0FF;
}

.delete,
.cancel {
  background-color: #d9534f;
}

.delete:hover,
.cancel:hover {
  background-color: #BD5A51FC;
}

</style>