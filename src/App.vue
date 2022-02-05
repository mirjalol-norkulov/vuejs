<template>
  <div id="app">
    <QuizzApp />
  </div>
</template>

<script>
import QuizzApp from "./components/QuizzApp.vue";

export default {
  name: "App",
  components: { QuizzApp },
  data() {
    return {};
  },
  computed: {},
  watch: {},
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

body {
  font-family: "Helvetica", sans-serif;
  margin: 0;
}
</style>
