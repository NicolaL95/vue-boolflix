<template>
  <div id="app">
    <Header @getQuery="passQuery"></Header>
    <Main :getAPI="obtainQuery"></Main>
  </div>
</template>

<script>
import Main from "./components/Main.vue";
import Header from "./components/Header.vue";
export default {
  name: "App",
  components: {
    Main,
    Header,
  },
  data() {
    return {
      obtainQuery: "",
    };
  },
  methods: {
    passQuery(query) {
      this.obtainQuery = query;
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}
</style>
