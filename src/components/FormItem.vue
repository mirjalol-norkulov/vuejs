<template>
  <div class="form-item">
    <label v-if="label" :for="name">{{ label }}</label>
    <input :id="name" v-bind="$attrs" v-on="$listeners" />
  </div>
</template>

<script>
export default {
  name: "FormItem",
  inheritAttrs: false,
  props: {
    name: {
      type: String,
      required: true
    },
    label: {
      type: String,
      default: undefined
    }
  }
}
</script>

<style lang="scss" scoped>
.form-item {
  display: flex;
}
</style>