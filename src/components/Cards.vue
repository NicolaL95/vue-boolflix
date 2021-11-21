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
        <p class="title"><span>Titolo:</span> {{ titleMovie }}</p>
        <p class="original_title">
          <span>Titolo Originale:</span> {{ titleMovieO }}
        </p>
        <div class="len">
          <span>Lingua:</span>
          <Flag :selCountry="country" />
        </div>
        <div class="rate">
          <span>Voto:</span>
          <Star :votes="voteAverage"></Star>
        </div>
        <p class="desc">{{ desc }}</p>
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
        <p class="title"><span>Titolo:</span> {{ titleTv }}</p>
        <p class="original_title">
          <span>Titolo Originale:</span> {{ titleTvO }}
        </p>
        <div class="len">
          <span>Lingua: </span>
          <Flag :selCountry="country" />
        </div>
        <div class="rate">
          <span>Voto: </span>
          <Star :votes="voteAverage"></Star>
        </div>
        <p class="desc">{{ desc }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Flag from "./Flag.vue";
import Star from "./Star.vue";
export default {
  components: {
    Flag,
    Star,
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
.movie_container:hover .cover,
.tv_container:hover .cover {
  filter: brightness(0);
}

.cards:hover .multimedia_content {
  display: block;
  position: absolute;
  top: 0;
  left: 0;
}
</style>