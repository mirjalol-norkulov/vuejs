<template>
  <div class="digital-clock">
    <span class="digital-clock__item">{{ hour }}</span>
    <span class="digital-clock__item">{{ minute }}</span>
    <span class="digital-clock__item">{{ seconds }}</span>
  </div>
</template>

<script>
export default {
  name: "DigitalClock",
  data() {
    return {
      hour: "",
      minute: "",
      seconds: "",
    };
  },
  beforeCreate() {
    console.group("beforeCreate");
    console.log("this: ", this);
    console.log("this: ", this.$data);
    console.groupEnd();
  },
  updated() {
    console.log("Component updated");
  },
  created() {
    this.updateClockData();
    this.intervalId = setInterval(this.updateClockData, 1000);
  },
  mounted() {
    console.log(this.$attrs);
    console.log(this.$listeners);
  },
  beforeDestroy() {
    console.log('Before destroy');
    if (this.intervalId) {
      clearInterval(this.intervalId)
    }
  },
  methods: {
    updateClockData() {
      const date = new Date();
      this.hour = date.getHours().toString().padStart(2, "0");
      this.minute = date.getMinutes().toString().padStart(2, "0");
      this.seconds = date.getSeconds().toString().padStart(2, "0");
    }
  }
};
</script>

<style lang="scss">
.digital-clock {
  display: flex;

  &__item {
    display: inline-block;
    padding: 1rem;
    background: #000;
    color: #fff;
  }
}
</style>
