<template>
  <div id="main_container">
    <div
      class="multimedia"
      v-for="multimedia in multimedias"
      :key="multimedia.id"
    >
      <div v-if="multimedia.genre == 'film'" class="movie_container">
        <h1>FILM</h1>
        <p class="title">{{ multimedia.title }}</p>
        <p class="original_title">{{ multimedia.original_title }}</p>
        <Flag :selCountry="multimedia.original_language" />
        <p class="original_language">{{ multimedia.original_language }}</p>
        <p class="vote_average">{{ multimedia.vote_average }}</p>
        <img
          :src="'https://image.tmdb.org/t/p/w342' + multimedia.backdrop_path"
        />
        <Star :votes="multimedia.vote_average"></Star>
      </div>

      <div v-else class="tv_container">
        <h1>SERIE TV</h1>
        <p class="name">{{ multimedia.title }}</p>
        <p class="original_name">{{ multimedia.original_title }}</p>
        <Flag :selCountry="multimedia.original_language" />
        <p class="original_language">{{ multimedia.original_language }}</p>
        <p class="vote_average">{{ multimedia.vote_average }}</p>
        <img
          :src="'https://image.tmdb.org/t/p/w342' + multimedia.backdrop_path"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
/* import Header from "./Header.vue"; */
import Flag from "./Flag.vue";
import Star from "./Star.vue";
export default {
  components: {
    Flag,
    Star,
  },
  data() {
    return {
      customQuery: "",
      multimedias: [],
    };
  },
  watch: {
    /* get two Apis and merge them in an array  */
    getAPI: function (val) {
      console.log(val);
      this.multimedias = [];
      console.log("ciao");
      const API_URLF =
        "https://api.themoviedb.org/3/search/movie?api_key=fd4723f70e60dc27b6383adc8e7700ec&query=" +
        val;
      const API_URLT =
        "https://api.themoviedb.org/3/search/tv?api_key=fd4723f70e60dc27b6383adc8e7700ec&query=" +
        val;
      axios.all([axios.get(API_URLF), axios.get(API_URLT)]).then((r) => {
        /* set properties to specify type of content and add to array multimedias */
        r[0].data.results.forEach((element) => {
          element.genre = "film";
          this.multimedias.push(element);
        });
        r[1].data.results.forEach((element) => {
          element.genre = "tv";
          this.multimedias.push(element);
        });
      });
      console.log(this.multimedias);
      //call your method here
    },
  },
  props: {
    getAPI: String,
  },
  mounted() {
    this.customQuery = this.getAPI;
  },
  methods: {},
};
</script>

<style lang="scss">
#main_container {
  background-color: #434343;
}
</style>