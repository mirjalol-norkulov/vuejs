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
    return {
      showClock: true,
    };
  },
  computed: {},
  watch: {},
};
</script>
