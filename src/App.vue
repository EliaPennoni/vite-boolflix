<script>
import axios from "axios";
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import AppFooter from "./components/AppFooter.vue";
import { store } from "./store";
export default {
  data() {
    return {
      searchText: "",
      apiKey: "7142d541a997e6c5a2224e574d25f0ba",
      movies: [],
      series: [],
      store,
    };
  },
  methods: {
    searchMovie() {
      axios
        .get("https://api.themoviedb.org/3/search/movie", {
          params: {
            api_key: this.apiKey,
            query: this.store.searchText,
          },
        })
        .then((resp) => {
          console.log(resp.data.results);
          this.store.movies = resp.data.results;
        })
        .catch((error) => {
          console.error("Errore nella richiesta API:", error); // Gestione degli errori
        });
      axios
        .get("https://api.themoviedb.org/3/search/tv", {
          params: {
            api_key: this.apiKey,
            query: this.store.searchText,
          },
        })
        .then((resp) => {
          console.log(resp.data.results);
          this.store.series = resp.data.results;
        })
        .catch((error) => {
          console.error("Errore nella richiesta API:", error); // Gestione degli errori
        });
    },
  },
  computed: {},
  components: {
    AppHeader,
    AppMain,
    AppFooter,
  },
};
</script>

<template>
  <AppHeader @searchMovie="searchMovie()" />

  <AppMain :movies="store.movies" :series="store.series" />

  <AppFooter />
</template>

<style lang="scss" scoped>
@import "bootstrap/scss/bootstrap";
</style>
