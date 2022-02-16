<template>
  <div class="quizz-item" :class="{ 'quizz-item--selected': quizz.userAnswer }">
    <div class="quizz-item__question">{{ index }}. {{ quizz.question }}</div>
    <section>
      <label
        v-for="(option, optionIndex) in quizz.options"
        :key="optionIndex"
        :for="`quizz-${index}-${optionIndex}`"
        class="quizz-item__option"
        :class="{ 'quizz-item__option--selected': option === quizz.userAnswer }"
      >
        {{ "abcde"[optionIndex] }}) {{ option }}
        <input
          type="radio"
          :id="`quizz-${index}-${optionIndex}`"
          :value="option"
          v-model="userAnswer"
          @change="inputChange"
        />
      </label>
    </section>
  </div>
</template>

<script>
export default {
  name: "QuizzItem",
  props: {
    quizz: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      userAnswer: null,
    };
  },
  watch: {
    quizz: {
      immediate: true,
      deep: true,
      handler(newValue) {
        this.userAnswer = newValue.userAnswer;
      },
    },
  },
  methods: {
    inputChange(event) {
      this.$emit("user-answer-change", {
        id: this.quizz.id,
        answer: event.target.value,
      });
    },
  },
};
</script>

<style lang="scss">
@import "@/assets/quizz.scss";

.quizz-item {
  border-bottom: dotted 4px lightgray;

  &--selected {
    border-left: solid 4px $quizz-color;
  }

  &__question {
    padding: 2rem 1rem;
  }

  &__option {
    padding: 1.5rem 1rem;
    transition: all 0.3s;
    display: block;
    cursor: pointer;

    input {
      display: none;
    }

    &:not(&--selected):hover {
      background: $quizz-color;
      color: #fff;
    }

    &--selected {
      padding-top: 2rem;
      padding-bottom: 2rem;
      background: #36312c;
      color: #fff;
    }
  }
}
</style>
