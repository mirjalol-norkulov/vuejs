<template>
  <button
    class="base-button"
    :class="{
      'base-button--success': color === 'success',
      'base-button--warning': color === 'warning',
      'base-button--danger': color === 'danger'
    }"
  >{{ text }}</button>
</template>

<script>
export default {
  name: "BaseButton",
  props: {
    text: {
      type: String,
      default: ""
    },
    color: {
      type: String,
      default: "success",
      validator(color) {
        if (!["success", "warning", "danger"].includes(color)) {
          console.error("Invalid color value: ", color);
          return false;
        }

        return true;
      }
    }
  }
}
</script>

<style lang="scss">
.base-button {
  padding: 0.5rem 3rem;
  color: #fff;

  &--success {
    background-color: lightgreen;
  }

  &--warning {
    background-color: orange;
  }

  &--danger {
    background-color: red;
  }
}
</style>