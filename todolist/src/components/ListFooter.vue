<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" :checked="isAll" @change="checkAll"/>
      <span>
      Finish {{ doneTotal }}/ All {{ total }}
      </span>
    </label>
    <button class="list-item-button" @click="clearAll">Delete aLl finished tasks</button>
  </div>
</template>

<script>
export default {
  name: "ListFooter",
  props: ["todos", "checkAllTodo", "clearAllTodo"],
  computed: {
    total() {
      return this.todos.length
    },
    doneTotal() {
      return this.todos.reduce((pre, current) => {
        return pre + (current.done ? 1 : 0)
      }, 0)
    },
    isAll() {
      return this.doneTotal === this.total && this.total > 0
    }
  },
  methods: {
    checkAll(e) {
      this.checkAllTodo(e.target.checked)
    },
    clearAll() {
      this.clearAllTodo()
    }
  }
}
</script>

<style scoped>
.list-item-button {
  background-color: #d9534f;
  color: white;
  border: none;
  padding: 0.8vh 1vw;
  border-radius: 5px;
}

.todo-footer {
  display: flex;
  justify-content: space-between;

  margin: 2vh auto;
}

</style>