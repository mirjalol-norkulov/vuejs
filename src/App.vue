<template>
  <div id="app">
    <input v-model="newTodoContent" @keyup.enter="addTodo" />
    <todo-item
      v-for="todo in filteredTodos"
      :key="todo.id"
      :todo="todo"
      @checkbox-click="changeComplete(todo.id)"
    />

    <div>{{ activeCountText }}</div>
    <div class="filter">
      <div
        v-for="filterItem in filters"
        :key="filterItem"
        class="filter__item"
        :class="{ 'filter__item--active': filter === filterItem }"
      >
        <input
          type="radio"
          v-model="filter"
          :value="filterItem"
          :id="filterItem"
          class="filter__input"
        />
        <label :for="filterItem" class="filter__label">{{ filterItem }}</label>
      </div>
    </div>

    <button @click="clearCompleted">Clear completed</button>
  </div>
</template>

<script>
// custom event
import TodoItem from "./components/TodoItem";

export default {
  name: "App",
  components: {
    TodoItem
  },
  data() {
    return {
      filters: ["ALL", "COMPLETED", "ACTIVE"],
      filter: "ALL",
      todos: [
        { id: 1, content: "Dars o'tish", completed: true },
        { id: 2, content: "Kechki ovqatni yeyish", completed: true },
      ],
      newTodoContent: ""
    }
  },
  computed: {
    activeCountText() {
      const count = this.todos.filter(todo => !todo.completed).length;
      if (count === 1) {
        return "1 item left";
      }
      return `${count} items left`;
    },
    filteredTodos() {
      if (this.filter === "ALL") {
        return this.todos;
      }

      return this.todos.filter(todo => this.filter === "COMPLETED" ? todo.completed : !todo.completed)
    }
  },
  methods: {
    changeComplete(todoId) {
      this.todos = this.todos.map(todo => {
        if (todo.id === todoId) {
          return { ...todo, completed: !todo.completed }
        } else {
          return todo;
        }
      })
    },
    clearCompleted() {
      this.todos = this.todos.filter(todo => !todo.completed)
    },
    addTodo(event) {
      if (event.key === "Enter") {
        this.todos.push({
          id: this.todos.length + 1,
          content: this.newTodoContent,
          completed: false
        })
      }
    }
  }
};

</script>

<style lang="scss">
.filter {
  display: flex;

  &__item {
    display: flex;
    align-items: center;
    cursor: pointer;
  }

  &__item--active {
    border: solid 1px gray;
    border-radius: 4px;
  }

  &__input {
    display: none;
  }

  &__label {
    cursor: pointer;
    padding: 5px 10px;
  }
}
</style>