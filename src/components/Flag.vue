<template>
  <div>
    <country-flag v-bind:country="selCountry" size="normal" />
  </div>
</template>

<script>
import CountryFlag from "vue-country-flag";
export default {
  components: {
    CountryFlag,
  },
  props: {
    selCountry: String,
  },
};
</script>

<style>
</style>