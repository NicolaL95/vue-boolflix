<template>
  <div id="header_container">
    <h1>BOOLFLIX</h1>
    <div class="input">
      <input
        v-model="customQuery"
        type="text"
        @keyup.enter="$emit('getQuery', customQuery), cleanInput()"
      />
      <label for="genre">Genere:</label>
      <select
        name="fil_gen"
        id="#filter_genre"
        v-model="selectGenre"
        placeholder="All"
        @change="$emit('find', selectGenre)"
      >
        <option :value="allgenre">All</option>
        <option v-for="genre in gerneList" :key="genre.id" :value="genre.id">
          {{ genre.name }}
        </option>
      </select>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      customQuery: "",
      gerneList: [],
      selectGenre: 0,
      allgenre: 0,
    };
  },
  mounted() {
    const genAPI =
      "https://api.themoviedb.org/3/genre/movie/list?api_key=fd4723f70e60dc27b6383adc8e7700ec";
    axios.get(genAPI).then((r) => {
      this.gerneList = r.data.genres;
    });
  },

  methods: {
    cleanInput() {
      this.customQuery = "";
      this.selectGenre = 0;
    },
  },
};
</script>

<style lang="scss">
#header_container {
  background-color: black;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  padding: 5px 20px;
  h1 {
    color: #920000;
    font-size: 1.5rem;
    margin: 10px 0 5px;
  }

  .input {
    height: 25px;
    margin: 10px 0 5px;
    label {
      margin: 0 10px 0 20px;
      color: white;
    }
  }
}
</style>