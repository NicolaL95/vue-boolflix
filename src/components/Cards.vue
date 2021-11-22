<template>
  <div class="cards">
    <div v-if="genre == 'film'" class="movie_container">
      <img
        class="cover"
        v-if="imgSrc != null"
        :src="'https://image.tmdb.org/t/p/w342' + imgSrc"
      />
      <img class="cover" v-else src="../assets/not-found.jpg" alt="" />
      <div class="multimedia_content">
        <div :class="{ inactive: isActor }" class="isOverview">
          <p class="title"><span>Titolo:</span> {{ titleMovie }}</p>
          <p class="original_title">
            <span>Titolo Originale:</span> {{ titleMovieO }}
          </p>
          <div class="advanced d-flex">
            <div class="components_data">
              <div class="len">
                <span>Lingua:</span>
                <Flag :selCountry="country" />
              </div>
              <div class="rate">
                <span>Voto:</span>
                <Star :votes="voteAverage"></Star>
              </div>
            </div>
            <button
              v-on:click="getActors(multimediaId)"
              class="actors actors_button"
            >
              Attori:
            </button>
          </div>

          <p class="desc">{{ desc }}</p>
        </div>
        <div :class="{ active: isActor }" class="isActors">
          <h5>Cast:</h5>
          <div v-for="actor in aActors" :key="actor.id" class="actor">
            <p class="mb-1">{{ actor.name }} as {{ actor.character }}</p>
          </div>
          <div class="button_overview d-flex justify-content-center mt-2">
            <button class="actors_button" v-on:click="getDesc()">
              Overview
            </button>
          </div>
        </div>
      </div>
    </div>
    <div v-else class="tv_container">
      <img
        class="cover"
        v-if="imgSrc != null"
        :src="'https://image.tmdb.org/t/p/w342' + imgSrc"
      />
      <img class="cover" v-else src="../assets/not-found.jpg" alt="" />
      <div class="multimedia_content">
        <div :class="{ inactive: isActor }" class="isOverview">
          <p class="title"><span>Titolo:</span> {{ titleTv }}</p>
          <p class="original_title">
            <span>Titolo Originale:</span> {{ titleTvO }}
          </p>
          <div class="advanced d-flex">
            <div class="components_data">
              <div class="len">
                <span>Lingua:</span>
                <Flag :selCountry="country" />
              </div>
              <div class="rate">
                <span>Voto:</span>
                <Star :votes="voteAverage"></Star>
              </div>
            </div>
            <button
              v-on:click="getActors(multimediaId)"
              class="actors actors_button"
            >
              Attori:
            </button>
          </div>
          <p class="desc">{{ desc }}</p>
        </div>
        <div :class="{ active: isActor }" class="isActors">
          <h5>Cast:</h5>
          <div v-for="actor in aActors" :key="actor.id" class="actor">
            <p class="mb-1">{{ actor.name }} as {{ actor.character }}</p>
          </div>
          <div class="button_overview d-flex justify-content-center mt-2">
            <button class="actors_button" v-on:click="getDesc()">
              Overview
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Flag from "./Flag.vue";
import Star from "./Star.vue";
import axios from "axios";
export default {
  components: {
    Flag,
    Star,
  },
  data() {
    return {
      aActors: [],
      isActor: false,
    };
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
    desc: String,
    multimediaId: Number,
  },
  methods: {
    getActors(id) {
      this.aActors = [];
      let actorAPI;
      if (this.genre == "film") {
        actorAPI = `https://api.themoviedb.org/3/movie/${id}/credits?api_key=fd4723f70e60dc27b6383adc8e7700ec`;
      } else {
        actorAPI = `https://api.themoviedb.org/3/tv/${id}/credits?api_key=fd4723f70e60dc27b6383adc8e7700ec`;
      }
      axios.get(actorAPI).then((r) => {
        this.aActors = r.data.cast;
        this.aActors.length = 5;
        this.isActor = true;
      });
    },
    getDesc() {
      this.isActor = false;
    },
  },
};
</script>

<style lang="scss">
.cards {
  border: 1px solid white;
  position: relative;
  .multimedia_content {
    display: none;
  }
}

.multimedia_content {
  padding: 5px;
  color: white;
  max-height: 192px;
  overflow: overlay;
  width: 100%;
  p {
    margin: 0;
  }

  span {
    font-weight: bold;
    display: inline-block;
    padding-right: 4px;
  }
  .rate {
    #stars {
      display: inline-block;
      .star_color {
        color: goldenrod;
      }
    }
  }
  .len {
    #flag_type {
      display: inline-block;
      img {
        width: 30px;
      }
    }
  }
}

.multimedia_content::-webkit-scrollbar {
  border-radius: 10px;
}

/* HOVER */
.cards:hover .cover {
  filter: brightness(0);
}

.cards:hover .multimedia_content {
  display: block;
  position: absolute;
  top: 0;
  left: 0;
}

.actors_button {
  height: 34px;
  border: 0;
  color: gray;
  background-color: white;
  border-radius: 25px;
  padding: 0 13px;
}

.actors {
  margin-left: 85px;

  margin-top: 5px;
}
.isActors {
  display: none;
}
.active {
  display: block;
}

.inactive {
  display: none;
}
</style>
