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
      <QuizzSiderClock v-show="value" :minutes="20" @finish="$emit('finish')" />
    </header>

    <main v-show="value" class="quizz-sider__main">
      <section class="quizz-sider__top">
        <span class="quizz-sider__subject">Matematika</span>
        <div>
          {{ selectedCount }} /
          {{ quizzes.length }}
        </div>
      </section>

      <section class="quizz-sider__buttons">
        <button
          v-for="(quizz, index) in quizzes"
          :key="quizz.id"
          class="quizz-sider__button"
          :class="{ 'quizz-sider__button--active': !!quizz.userAnswer }"
          @click="handleButtonClick(quizz)"
        >
          {{ index + 1 }}
        </button>
      </section>
    </main>
  </aside>
</template>

<script>
import { Icon } from "@v2icons/utils";
import { ChevronLeftFilled, ChevronRightFilled } from "@v2icons/material";
import QuizzSiderClock from "./QuizzSiderClock.vue";

export default {
  name: "QuizzSider",
  components: { Icon, ChevronLeftFilled, ChevronRightFilled, QuizzSiderClock },
  props: {
    value: {
      type: Boolean,
      default: false,
    },
    quizzes: {
      type: Array,
      required: true,
    },
  },
  computed: {
    selectedCount() {
      return this.quizzes.filter((quizz) => !!quizz.userAnswer).length;
    },
  },
  methods: {
    toggleSider() {
      this.$emit("input", !this.value);
    },
    handleButtonClick(quizz) {
      this.$emit("quizz-click", quizz);
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

  &__main {
    padding: 1rem;
  }

  &__top {
    display: flex;
    justify-content: space-between;
    padding: 0.5rem 0;
    border-bottom: 2px dotted rgba(87, 87, 87, 0.12);
    margin-bottom: 0.5rem;
  }

  &__subject {
    font-weight: bold;
  }

  &__buttons {
    display: flex;
    flex-wrap: wrap;
  }

  &__button {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    border: solid 1px black;
    background: transparent;

    &:hover,
    &--active {
      background: black;
      color: #fff;
    }

    &:not(:first-child) {
      margin-left: 5px;
    }
  }
}

.quizz-sider-clock {
  flex: 1;
}
</style>
