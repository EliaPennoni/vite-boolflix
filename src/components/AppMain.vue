<script>
import axios from "axios";
import SingleMovie from "./SingleMovie.vue";
import { store } from "../store";
export default {
  data() {
    return {
      searchText: "",
      apiKey: "7142d541a997e6c5a2224e574d25f0ba",
      store,
    };
  },
  props: {
    movies: Array,
    series: Array,
  },
  components: {
    SingleMovie,
  },
  methods: {
    searchMovie() {
      console.log("cerca il film");

      axios
        .get("https://api.themoviedb.org/3/search/movie", {
          params: {
            api_key: this.apiKey,
            query: this.searchText,
          },
        })
        .then((resp) => {
          console.log(resp.data.results);
          this.movies = resp.data.results;
        })
        .catch((error) => {
          console.error("Errore nella richiesta API:", error); // Gestione degli errori
        });
      axios
        .get("https://api.themoviedb.org/3/search/tv", {
          params: {
            api_key: this.apiKey,
            query: this.searchText,
          },
        })
        .then((resp) => {
          console.log(resp.data.results);
          this.series = resp.data.results;
        })
        .catch((error) => {
          console.error("Errore nella richiesta API:", error); // Gestione degli errori
        });
    },
    flagPusher(lang) {
      const validLang = ["it", "en", "ja"];
      if (validLang.includes(lang)) {
        if (lang === "it") {
          return "../it-flag.gif";
        } else if (lang === "en") {
          return "../us-flag.gif";
        } else if (lang === "ja") {
          return "../ja-flag.gif";
        }
      }
      return "../CalicoJack-3.jpg";
    },
  },
};
</script>

<template>
  <main>
    <h2>Movies</h2>
    <div class="movies">
      <div class="row g-3 info">
        <div
          v-for="(movie, index) in store.movies"
          :key="index"
          class="size col-12 col-sm-6 col-md-4 col-lg-3 mt-3 mb-5"
        >
          <SingleMovie
            :title="movie.title"
            :originalTitle="movie.original_title"
            :language="movie.original_language"
            :rating="movie.vote_average"
            :plot="movie.overview"
            :posterPath="movie.poster_path"
          />
        </div>
      </div>
    </div>
    <h2>Tv Series</h2>
    <div class="series">
      <div class="row g-3">
        <div
          v-for="(serie, index) in store.series"
          :key="index"
          class="col-12 col-sm-6 col-md-4 col-lg-3 mt-3"
        >
          <SingleMovie
            :title="serie.name"
            :originalTitle="serie.original_title"
            :language="serie.original_language"
            :rating="serie.vote_average"
            :plot="serie.overview"
            :posterPath="serie.poster_path"
          />
        </div>
      </div>
    </div>
  </main>
</template>

<style lang='scss' scoped>
@import "bootstrap/scss/bootstrap";
main {
  background-color: black;
}
h2 {
  color: white;
  font-weight: bold;
}
</style>
