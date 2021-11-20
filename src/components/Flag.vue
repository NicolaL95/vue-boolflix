<template>
  <div>
    <img :src="require('../assets/flag/' + selCountry + '.png')" alt="" />
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