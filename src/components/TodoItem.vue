<template>
  <div class="todo-item" :class="{ 'todo-item--completed': todo.completed }">
    <input type="checkbox" :checked="todo.completed" @change="onCheckboxChange" />
    <input
      v-if="isEditing"
      ref="input"
      class="todo-item__input"
      v-model="newTodoContent"
      @blur="deactivateEditMode"
      @keyup.esc="deactivateEditMode"
      @keyup.enter="onTodoContentChange"
    />
    <div v-else class="todo-item__content" @dblclick="activateEditMode">{{ todo.content }}</div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    todo: {
      type: Object,
      required: true,
      validator(todo) {
        if (!todo.id) {
          console.error('id mavjud emas')
          return false;
        }

        return true;
      }
    }
  },
  data() {
    return {
      newTodoContent: '',
      isEditing: false
    }
  },
  methods: {
    onCheckboxChange() {
      this.$emit('checkbox-click');
    },
    onTodoContentChange() {
      this.$emit('edit', this.newTodoContent);
      this.isEditing = false;
    },
    activateEditMode() {
      this.isEditing = true;
      this.newTodoContent = this.todo.content;
      this.$nextTick(() => {
        this.$refs.input.focus();
      })
    },
    deactivateEditMode() {
      this.isEditing = false;
    }
  }
}
</script>

<style lang="scss">
.todo-item {
  padding: 8px 4px;
  border-bottom: solid 1px lightgray;
  font-size: 24px;
  color: #4d4d4d;
  display: flex;
  align-items: center;

  &--completed {
    .todo-item__content {
      text-decoration: line-through;
    }
  }

  &__input {
    border: 0;
    outline: none;
    font-size: inherit;
    color: inherit;
  }

  &__content {
    flex-grow: 1;
  }
}
</style>