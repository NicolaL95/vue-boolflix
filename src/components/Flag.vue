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
      /* Check in flag folder if value of country returns a specific flag(value - name.png) if not, return a placeholder img */
      const flagList = require.context("../assets/flag", true, /^.*\.png$/);
      if (flagList.keys().includes(`./${this.selCountry}.png`)) {
        return this.selCountry;
      } else {
        return "placeholder";
      }
    },
  },
};
</script>

<style>
</style>