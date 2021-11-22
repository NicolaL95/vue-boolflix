<template>
  <div id="main_container">
    <div class="cards_container">
      <Cards
        v-for="multimedia in multimedias"
        :key="multimedia.id"
        :genre="multimedia.genre"
        :titleMovie="multimedia.title"
        :titleMovieO="multimedia.original_title"
        :country="multimedia.original_language"
        :voteAverage="multimedia.vote_average"
        :imgSrc="multimedia.poster_path"
        :titleTv="multimedia.name"
        :titleTvO="multimedia.original_name"
        :desc="multimedia.overview"
        :multimediaId="multimedia.id"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Cards from "./Cards.vue";
export default {
  components: {
    Cards,
  },
  data() {
    return {
      customQuery: "",
      multimedias: [],
      multimedias_all: [],
    };
  },
  watch: {
    /* get two Apis and merge them in an array  */
    getAPI: function (val) {
      this.multimedias = [];
      this.multimedias_all = [];
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
          this.multimedias_all.push(element);
        });
        r[1].data.results.forEach((element) => {
          element.genre = "tv";
          this.multimedias.push(element);
          this.multimedias_all.push(element);
        });
      });
      this.customQuery = "";
    },
    getGenre: function (val) {
      this.multimedias = [];
      for (let i = 0; i < this.multimedias_all.length; i++) {
        this.multimedias.push(this.multimedias_all[i]);
        if (val != 0) {
          this.multimedias.forEach((element, index) => {
            if (!element.genre_ids.includes(val)) {
              this.multimedias.splice(index, 1);
            }
          });
        }
      }
    },
  },
  props: {
    getAPI: String,
    getGenre: String,
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
  min-height: calc(100vh - 54px);
  .cards_container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px 30px;
    padding: 30px;
  }
}
</style>