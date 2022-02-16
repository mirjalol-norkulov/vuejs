<template>
  <div class="quizz-sider-clock">
    <span>{{ hour }} : </span>
    <span>{{ minute }} : </span>
    <span>{{ second }}</span>
  </div>
</template>

<script>
export default {
  name: "QuizzSiderClock",
  props: {
    minutes: {
      type: Number,
      default: 20,
    },
  },
  data() {
    return {
      currentSecond: 0,
    };
  },
  watch: {
    minutes: {
      immediate: true,
      handler() {
        this.currentSecond = this.minutes * 60;
      },
    },
  },
  computed: {
    hour() {
      return Math.floor(this.currentSecond / 3600)
        .toString()
        .padStart(2, "0");
    },
    minute() {
      return Math.floor(this.currentSecond / 60)
        .toString()
        .padStart(2, "0");
    },
    second() {
      return (this.currentSecond % 60).toString().padStart(2, "0");
    },
  },
  created() {
    this.intervalId = setInterval(() => {
      if (this.currentSecond === 0) {
        this.$emit("finish");
        clearInterval(this.intervalId);
      } else {
        this.currentSecond--;
      }
    }, 1000);
  },
  beforeDestroy() {
    if (this.intervalId) {
      clearInterval(this.intervalId);
    }
  },
};
</script>

<style lang="scss">
.quizz-sider-clock {
  font-size: 30px;
  text-align: center;
}
</style>
