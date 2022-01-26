<template>
  <div>
    <input type="checkbox" :checked="todo.completed" @change="onCheckboxChange" />
    {{ todo.content }}
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ['todo'],
  methods: {
    onCheckboxChange() {
      this.$emit('checkbox-click');
    }
  }
}
</script>