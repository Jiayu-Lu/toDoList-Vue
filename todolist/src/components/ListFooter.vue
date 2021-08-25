<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" :checked="isAll" @change="checkAll"/>
      <span>
      Finish {{ doneTotal }}/ All {{ total }}
      </span>
    </label>
    <b-progress :max="max" animated class="todo-progess">
      <b-progress-bar :value="value" :label="`${((value / max) * 100).toFixed(0)}%`"></b-progress-bar>
    </b-progress>
    <button class="list-item-button" @click="clearAll">Delete all finished tasks</button>
  </div>
</template>

<script>
export default {
  name: "ListFooter",
  props: ["todos", "checkAllTodo", "clearAllTodo"],
  data() {
    return {
      max: 100
    }
  },
  computed: {
    value() {
      if(this.total === 0) return 0
      return this.doneTotal / this.total * 100
    },
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
      if(confirm("are you sure to delete all finished tasks")) {
        this.clearAllTodo()
      }
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

.list-item-button:hover {
  background-color: #BD5A51FC;
}

.todo-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;

  margin: 2vh auto;
}

.todo-progess {
  width: 50%;
}

</style>