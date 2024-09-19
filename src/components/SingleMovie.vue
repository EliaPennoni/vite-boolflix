<script>
import axios from "axios";
export default {
  data() {
    return {
      searchText: "",
      apiKey: "7142d541a997e6c5a2224e574d25f0ba",
      movies: [],
      series: [],
      baseImg: "https://image.tmdb.org/t/p/",
      posterSize: "w342",
    };
  },
  props: {
    title: String,
    originalTitle: String,
    language: String,
    rating: Number,
    plot: String,
    posterPath: String,
  },
  created() {},
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
    starRaters() {},
  },
};
</script>

<template>
  <div class="flip-card">
    <div class="flip-card-inner">
      <!-- Poster del film (fronte della card) -->
      <div class="flip-card-front">
        <img
          :src="baseImg + posterSize + posterPath"
          alt="Poster"
          class="poster"
        />
      </div>
      <!-- Informazioni del film (retro della card) -->
      <div class="flip-card-back">
        <ul class="list-unstyled">
          <li>
            <strong>{{ title }}</strong>
          </li>
          <li>
            {{ originalTitle }}
          </li>
          <li class="flag">
            <img :src="flagPusher(language)" alt="Flag" />
          </li>
          <li>
            <i
              v-for="x in Math.ceil(rating / 2)"
              :key="x"
              class="fa-solid fa-star"
            ></i>
            <i
              v-for="x in 5 - Math.ceil(rating / 2)"
              :key="x"
              class="fa-regular fa-star"
            ></i>
          </li>
          <li>
            {{ plot }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style lang='scss' scoped>
@import "bootstrap/scss/bootstrap";

.flip-card {
  perspective: 1000px;
  width: 320px !important;
  height: 450px !important;
  border-radius: 20px;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.8s ease-in-out;
  transform-style: preserve-3d;
  border-radius: 20px;
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

/* Parte frontale della card */
.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  border-radius: 20px;
}

/* Immagine all'interno della card */
.flip-card-front img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 20px;
}

/* Parte posteriore della card */
.flip-card-back {
  background-color: black;
  color: white;
  transform: rotateY(180deg);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px;
  border-radius: 20px;
}

.flip-card-back ul {
  list-style: none;
  padding: 0;
  text-align: center;
}

.flip-card-back li {
  margin-bottom: 10px;
}
.flag img {
  max-width: 40px;
  max-height: 25px;
  object-fit: contain;
  margin-top: 10px;
}
.row {
  justify-content: center !important;
  align-items: flex-start !important;
}
</style>
