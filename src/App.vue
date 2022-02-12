<template>
  <div id="app">
    <!-- <TodoTable /> -->
    <BaseMenu :items="menuItems" />
  </div>
</template>

<script>
// import TodoTable from "./components/TodoTable.vue";
import BaseMenu from "./components/BaseMenu.vue";

export default {
  name: "App",
  components: { BaseMenu },
  data() {
    return {
      showClock: true,
      menuItems: [
        {
          title: "Development",
          key: "development",
          children: [
            {
              title: "Web development",
              link: "https://google.com",
              key: "web-development",
              children: [
                {
                  title: "Javascript",
                },
                {
                  title: "VueJS",
                },
              ],
            },
            {
              title: "Data science",
              link: "https://google.com",
              key: "data-science",
            },
          ],
        },
        {
          title: "Business",
          key: "business",
          children: [
            {
              title: "Communication",
              link: "https://google.com",
              key: "communication",
            },
            {
              title: "Management",
              link: "https://google.com",
              key: "management",
            },
          ],
        },
      ],
    };
  },
  computed: {},
  watch: {},
};
</script>
