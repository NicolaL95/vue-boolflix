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
        <p class="original_language">{{ movie.original_language }}</p>
        <p class="vote_average">{{ movie.vote_average }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      customQuery: "",
      movies: [],
    };
  },
  methods: {
    getURL() {
      const API_URL =
        "https://api.themoviedb.org/3/search/movie?api_key=fd4723f70e60dc27b6383adc8e7700ec&query=" +
        this.customQuery +
        "&language=en-US&page=1&include_adult=false";
      axios.get(API_URL).then((r) => {
        console.log(r.data.results);
        this.movies = r.data.results;
      });
    },
  },
};
</script>

<style>
</style>