<template>
  <div class="quizz" :class="{ 'quizz--sider-open': isSiderOpen }">
    <main class="quizz__main">
      <header class="quizz__header">Matematika</header>
      <div class="quizz__content">
        <QuizzItem
          v-for="(quizz, index) in quizzes"
          :key="quizz.id"
          :quizz="quizz"
          :index="index + 1"
          @user-answer-change="handleUserAnswerChange"
        ></QuizzItem>
      </div>
    </main>
    <QuizzSider v-model="isSiderOpen" />
  </div>
</template>

<script>
import QuizzSider from "./QuizzSider.vue";
import QuizzItem from "./QuizzItem";

export default {
  name: "QuizzApp",
  components: { QuizzSider, QuizzItem },
  data() {
    return {
      isSiderOpen: false,
      quizzes: [
        {
          id: 1,
          question: "Quyidagi ko‘paytmalardan qaysi biri 45 ga qoldiqsiz bo‘linadi?",
          options: ["39⋅18", "234⋅80", "35⋅61", "80⋅23"],
          correctAnswer: "234⋅80",
          userAnswer: "39⋅18",
        },
        {
          id: 2,
          question:
            "246*013579246∗013579 soni 99 ga bo‘linishi uchun yulduzchaning o‘rniga qanday raqam qo‘yilishi kerak?",
          options: ["8", "7", "0", "4"],
          correctAnswer: "8",
        },
      ],
    };
  },
  methods: {
    handleUserAnswerChange(data) {
      this.quizzes = this.quizzes.map((quizz) => {
        if (quizz.id === data.id) {
          return { ...quizz, userAnswer: data.answer };
        } else {
          return quizz;
        }
      });
    },
  },
};
</script>

<style lang="scss">
.quizz {
  .quizz__main {
    width: calc(100% - 65px);
    transition: width 0.5s;
  }

  &--sider-open {
    .quizz__main {
      width: calc(100% - 530px);
    }
  }

  &__header {
    text-align: center;
    height: 56px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-bottom: 2px solid rgba(87, 87, 87, 0.12);
  }

  &__content {
    width: 80%;
    margin: 0 auto;
  }
}
</style>
