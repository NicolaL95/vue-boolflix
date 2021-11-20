<template>
  <div>
    <div id="stars">
      <i class="fas fa-star" v-for="vote in convStar" :key="vote"> </i>
      <i class="far fa-star" v-for="vote in leftStar" :key="vote"></i>
    </div>
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
    votes: String,
  },
  mounted() {
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

<style>
</style>