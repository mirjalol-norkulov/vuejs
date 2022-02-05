<template>
  <aside class="quizz-sider" :class="{ 'quizz-sider--open': value }">
    <header class="quizz-sider__header">
      <button class="quizz-sider__btn" @click="toggleSider">
        <Icon v-if="!value" size="36">
          <ChevronLeftFilled />
        </Icon>
        <Icon v-else size="36">
          <ChevronRightFilled />
        </Icon>
      </button>
    </header>
  </aside>
</template>

<script>
import { Icon } from "@v2icons/utils";
import { ChevronLeftFilled, ChevronRightFilled } from "@v2icons/material";

export default {
  name: "QuizzSider",
  components: { Icon, ChevronLeftFilled, ChevronRightFilled },
  props: {
    value: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    toggleSider() {
      this.$emit("input", !this.value);
    },
  },
};
</script>

<style lang="scss">
@import "@/assets/quizz.scss";

.quizz-sider {
  position: fixed;
  top: 0;
  right: 0;
  width: 65px;
  height: 100vh;
  background: $quizz-color;
  transition: width 0.5s;

  &__header {
    height: 56px;
    display: flex;
  }

  &__btn {
    background: darken($quizz-color, 5%);
    border: 0;
    cursor: pointer;
    width: 100%;
  }

  &--open {
    width: 530px;

    .quizz-sider__btn {
      width: 65px;
    }
  }
}
</style>
