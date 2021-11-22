<template>
  <div id="app">
    <Header @getQuery="passQuery" @find="getGenre"></Header>
    <Main :getAPI="obtainQuery" :getGenre="selGen"></Main>
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
      selGen: "",
    };
  },
  methods: {
    passQuery(query) {
      this.obtainQuery = query;
    },
    getGenre(gen) {
      this.selGen = gen;
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
