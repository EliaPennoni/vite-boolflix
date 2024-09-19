<script>
import axios from "axios";
import { store } from "../store";
export default {
  data() {
    return {
      store,
    };
  },
};
</script>

<template>
  <header>
    <div class="container-fluid">
      <div class="row align-items-center">
        <!-- Logo e Navbar -->
        <div class="col-md-6 d-inline-flex align-items-center">
          <div class="logo p-2">
            <img
              src="../../public/storia-di-netflix-1024x576.jpg.webp"
              alt="Logo"
            />
          </div>
          <nav>
            <ul class="d-flex list-unstyled mb-0">
              <li class="px-2"><a href="#">Home</a></li>
              <li class="px-2"><a href="#">Movie</a></li>
              <li class="px-2"><a href="#">Series</a></li>
              <li class="px-2"><a href="#">Most Popular</a></li>
              <li class="px-2"><a href="#">My Netflix</a></li>
            </ul>
          </nav>
        </div>

        <!-- Icone a destra -->
        <div class="col-md-6 d-flex justify-content-end">
          <nav>
            <ul class="d-flex list-unstyled mb-0">
              <li class="px-2">
                <a href="#"><i class="fa-solid fa-magnifying-glass"></i></a>
              </li>
              <li class="px-2">
                <a href="#"><i class="fa-solid fa-user"></i></a>
              </li>
              <li class="px-2">
                <a href="#"><i class="fa-solid fa-bell"></i></a>
              </li>
              <li class="px-2">
                <a href="#"><i class="fa-solid fa-gear"></i></a>
              </li>
            </ul>
          </nav>
        </div>
      </div>

      <!-- Campo di ricerca -->
      <div class="row mt-3">
        <div class="col-md-12">
          <input
            type="text"
            v-model="store.searchText"
            class="form-control"
            placeholder="Titolo del film"
          />
          <button @click="$emit('searchMovie')" class="btn btn-primary mt-2">
            Invia
          </button>
        </div>
      </div>
    </div>
  </header>
</template>


<style lang='scss' scoped>
@import "bootstrap/scss/bootstrap";

/* Header styles */
header {
  background-color: #000; /* Sfondo nero */
  padding: 15px 0;
}

/* Stili per il logo */
.logo img {
  max-width: 100px;
}

/* Stili per i link della navbar */
nav ul li a {
  text-decoration: none;
  color: #fff;
  font-size: 16px;
}

nav ul li a {
  text-decoration: none;
  color: #fff;
  position: relative;
  padding-bottom: 5px;
}

nav ul li a::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0%;
  height: 2px;
  background-color: red;
  transition: width 0.3s ease-in-out;
}

nav ul li a:hover::after {
  width: 100%;
}

/* Stili per le icone */
nav ul li a i {
  color: #fff;
  font-size: 20px;
}
nav ul li a:hover {
  color: red;
  font-size: 20px;
}

nav ul {
  list-style-type: none;
}

/* Stile aggiuntivo per il bottone di ricerca */
.btn-primary {
  background-color: red;
  border: none;
}

div nav ul li a i:hover {
  color: red;
}
.form-control {
  background-color: #ccc;
  color: #000;
  border: none;
  border-bottom: 2px solid #ccc;
  padding: 5px;
  outline: none;
  transition: border-bottom-color 0.3s ease-in-out,
    background-color 0.3s ease-in-out;
}

.form-control:focus {
  background-color: #ccc;
  color: #000;
  border-bottom-color: red;
}
</style>


