<template>
  <div id="app">
    <Main></Main>
    <font-awesome-icon icon="user-secret" />
    <gb-flag code="fr" size="small" />
  </div>
</template>

<script>
import Main from "./components/Main.vue";

export default {
  name: "App",
  components: {
    Main,
  },
};
</script>

<style lang="scss">
</style>
