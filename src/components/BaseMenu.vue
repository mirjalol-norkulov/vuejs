<template>
  <div class="menu">
    <div v-for="item in items" :key="item.key" class="menu__item">
      {{ item.title }}
      <BaseMenu
        class="menu__item-child"
        v-if="item.children && item.children.length > 0"
        :items="item.children"
        :depth="depth + 1"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "BaseMenu",
  props: {
    items: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style lang="scss">
.menu {
  width: 260px;
  border: solid 1px #ccc;
  position: relative;

  &__item {
    padding: 0.5rem 1rem;
  }

  &__item-child {
    position: absolute;
    top: 0;
    left: 100%;
    display: none;
  }

  &__item:hover > &__item-child {
    display: block;
  }
}
</style>
