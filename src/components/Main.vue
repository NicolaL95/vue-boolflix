<template>
  <div id="main_container">
    <div class="input">
      <input v-model="customQuery" type="text" />
      <button v-on:click="getURL()" type="button">Click me!</button>
    </div>
    <div class="container">
      <div class="movie" v-for="movie in movies" :key="movie.id">
        <p class="title">{{ movie.title }}</p>
        <p class="original_title">{{ movie.original_title }}</p>
        <Flag :selCountry="movie.original_language" />
        <p class="original_language">{{ movie.original_language }}</p>
        <p class="vote_average">{{ movie.vote_average }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Flag from "./Flag.vue";
export default {
  components: {
    Flag,
  },
  data() {
    return {
      customQuery: "",
      movies: [],
    };
  },
  methods: {
    getURL() {
      const API_URLF =
        "https://api.themoviedb.org/3/search/movie?api_key=fd4723f70e60dc27b6383adc8e7700ec&query=" +
        this.customQuery +
        "&language=en-US&page=1&include_adult=false";
      const API_URLT =
        "https://api.themoviedb.org/3/search/tv?api_key=fd4723f70e60dc27b6383adc8e7700ec&query=" +
        this.customQuery +
        "&language=en-US&page=1&include_adult=false";
      axios.all([axios.get(API_URLF), axios.get(API_URLT)]).then((r) => {
        console.log(r[0].data.results, r[1].data.results);
        this.movies = r[0].data.results && r[1].data.results;
        console.log(this.movies);
      });
    },
  },
};
</script>

<style>
</style>