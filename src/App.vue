<template>
  <div id="app">
    <div class="main">
      <h1>{{ count }}</h1>
      <button @click="count++">+</button>
      <button @click="count--">-</button>
      <TicTacToe />
    </div>
  </div>
</template>

<script>
import TicTacToe from "./components/TicTacToe";

export default {
  name: "App",
  components: { TicTacToe },
  data() {
    return {
      count1: 1,
      user: {
        id: 1,
        name: 'Ali'
      }
    }
  },
  computed: {
    count: {
      get() {
        return this.count1;
      },
      set(value) {
        if (value < 0) {
          return;
        }
        localStorage.setItem("count", value);
        this.count1 = value;
      }
    }
  },
  watch: {
    count: (newValue, oldValue) => {
      console.log(`count1 ${oldValue} dan ${newValue} ga o'zgardi.`);
    },
    user: {
      immediate: true,
      deep: true,
      handler(newValue) {
        console.log('user: ', newValue);
      }
    }
  }
};

</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

body {
  font-family: "Helvetica", sans-serif;
}

.main {
  width: 50%;
  margin: 0 auto;
}
</style>