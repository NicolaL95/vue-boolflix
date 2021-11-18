<template>
  <div id="main_container">
    <div class="input"></div>
    <input v-model="query" type="text" />
    <button type="button">Click me!</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      customQuery: "",
      movies: [],
      API_URL_SM:
        "https://api.themoviedb.org/3/search/movie?api_key=fd4723f70e60dc27b6383adc8e7700ec&query=&language=en-US&page=1&include_adult=false",
    };
  },
  mounted() {
    axios.get(this.API_URL_SM).then((r) => {
      this.movies = r.data.response;
    });
  },
};
</script>

<style>
</style>