<template>
  <div class="cards">
    <div v-if="genre == 'film'" class="movie_container">
      <!--  <p class="title">{{ titleMovie }}</p>
      <p class="original_title">{{ titleMovieO }}</p>
      <Flag :selCountry="country" /> -->
      <img
        v-if="imgSrc != null"
        :src="'https://image.tmdb.org/t/p/w342' + imgSrc"
      />
      <img v-else src="../assets/not-found.jpg" alt="" />
      <!-- <Star :votes="voteAverage"></Star> -->
    </div>

    <div v-else class="tv_container">
      <!--   <p class="name">{{ titleTv }}</p>
      <p class="original_name">{{ titleTvO }}</p>
      <Flag :selCountry="country" /> -->
      <img
        v-if="imgSrc != null"
        :src="'https://image.tmdb.org/t/p/w342' + imgSrc"
      />
      <img v-else src="../assets/not-found.jpg" alt="" />
      <!-- <Star :votes="voteAverage"></Star> -->
    </div>
  </div>
</template>

<script>
/* import Flag from "./Flag.vue";
import Star from "./Star.vue"; */
export default {
  components: {
    /*  Flag,
    Star, */
  },
  props: {
    genre: String,
    titleMovie: String,
    titleMovieO: String,
    country: String,
    voteAverage: Number,
    imgSrc: String,
    titleTv: String,
    titleTvO: String,
  },
};
</script>

<style lang="scss">
.cards {
  margin: 5px 10px;
}
</style>