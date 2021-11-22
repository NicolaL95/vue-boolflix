<template>
  <div id="flag_type">
    <img
      :src="require('../assets/flag/' + isFlag + '.png')"
      @error="selCountry = 'en'"
      alt=""
    />
  </div>
</template>

<script>
export default {
  props: {
    selCountry: String,
  },
  computed: {
    isFlag() {
      const flagList = require.context("../assets/flag", true, /^.*\.png$/);
      if (flagList.keys().includes(`./${this.selCountry}.png`)) {
        console.log("torna fra");
        return this.selCountry;
      } else {
        console.log("non torna fra");
        return "placeholder";
      }
    },
  },
};
</script>

<style>
</style>