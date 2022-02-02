<template>
  <div class="todo-list">
    <h1 class="todo-list__title">todos</h1>
    <main class="todo-list__main">
      <input class="todo-list__input" v-model="newTodoContent" @keyup.enter="addTodo" />
      <todo-item
        v-for="todo in filteredTodos"
        :key="todo.id"
        :todo="todo"
        @checkbox-click="changeComplete(todo.id)"
        @edit="newContent => editTodo(todo.id, newContent)"
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

      <BaseButton text="Clear completed" color="danger" @click="clearCompleted"></BaseButton>
    </main>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
import BaseButton from "./BaseButton";

export default {
  name: 'TodoList',
  components: {
    TodoItem, BaseButton
  },
  data() {
    return {
      filters: ["ALL", "COMPLETED", "ACTIVE"],
      filter: "ALL",
      todos: [
        { id: 1, content: "Dars o'tish", completed: true },
        { id: 2, content: "Kechki ovqatni yeyish", completed: true }
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
    },
    editTodo(todoId, todoContent) {
      this.todos = this.todos.map(todo => {
        if (todo.id === todoId) {
          return { ...todo, content: todoContent }
        } else {
          return todo;
        }
      })
    }
  }
}
</script>

<style lang="scss">
.todo-list {
  &__title {
    color: #ead7d7;
    font-size: 96px;
    font-weight: 400;
    text-align: center;
    margin-bottom: 16px;
  }

  &__main {
    box-shadow: 0 4px 5px 0 rgba(0, 0, 0, 0.14),
      0 1px 10px 0 rgba(0, 0, 0, 0.12), 0 2px 4px -1px rgba(0, 0, 0, 0.2);
  }

  &__input {
    padding: 1rem;
    width: 100%;
    outline: none;
    border: 0;
    font-size: 24px;
  }
}

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