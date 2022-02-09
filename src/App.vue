<template>
  <div id="app">
    <FormItem label="Show clock" name="showClock" v-model="showClock" type="checkbox" />
    
    <DigitalClock v-if="showClock" class="clock" id="clock" @blur="() => { }" />
  </div>
</template>

<script>
import DigitalClock from "./components/DigitalClock.vue";
import FormItem from "./components/FormItem.vue";

export default {
  name: "App",
  components: { DigitalClock, FormItem },
  data() {
    return {
      showClock: true
    };
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

.clock {
}
</style>
