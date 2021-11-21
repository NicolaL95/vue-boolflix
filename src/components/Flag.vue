<template>
  <div id="flag_type">
    <img
      :src="require('../assets/flag/' + selCountry + '.png')"
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
};
</script>

<style>
</style>