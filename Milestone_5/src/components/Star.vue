<template>
  <div id="stars">
    <i class="fas fa-star star_color" v-for="vote in convStar" :key="vote"> </i>
    <i class="far fa-star star_color" v-for="vote in leftStar" :key="vote"></i>
  </div>
</template>

<script>
export default {
  data() {
    return {
      convStar: "",
      leftStar: "",
    };
  },
  props: {
    votes: Number,
  },
  mounted() {
    /* Generate star full&empty based on vote_average */
    this.convStar = Math.ceil(this.votes / 2);
    this.leftStar = 5 - this.convStar;
  },
  computed: {
    getnum(votes) {
      return votes;
    },
  },
};
</script>

<style lang="scss">
</style>