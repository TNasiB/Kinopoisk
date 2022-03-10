<template>
  <div id="app">
    <HeaderComponent @get-films="getFilms" @send-query="getQuery" @sort-films="sortFilms"/>
    <FilmsWrapper :query="query" :films="films" @show-modal="showModal"/>
    <ModalFilm :film="this.film"></ModalFilm>
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComp';
import FilmsWrapper from './components/FilmsWrapper';
import ModalFilm from './components/ModalFilm';

export default {
  name: 'App',
  components: {
    HeaderComponent,
    FilmsWrapper,
    ModalFilm,
  },
  data() {
    return {
      films: [],
      query: "",
      film: {}
    }
  },
  methods: {
    showModal(film) {
      this.film = film
    },
    sortFilms() {
      this.films.sort((a, b) => a.rating > b.rating? -1 : 1)
    },
    getQuery(query) {
      fetch(`https://kinopoiskapiunofficial.tech/api/v2.1/films/search-by-keyword?keyword=${query}&page=1`, {
          method: 'GET',
          headers: {
              'X-API-KEY': '',//Введите свой ключ от Api
              'Content-Type': 'application/json',
          },
      })
      .then(res => res.json())
      .then(json => this.films = json.films)
    },
    getFilms() {
      fetch(`https://kinopoiskapiunofficial.tech/api/v2.2/films/top?type=TOP_100_POPULAR_FILMS`, {
          method: 'GET',
          headers: {
              'X-API-KEY': '', //Введите свой ключ от Api
              'Content-Type': 'application/json',
          },
      })
      .then(res => res.json())
      .then(json => this.films = json.films)
    },
  },
  beforeCreate() {
    fetch(`https://kinopoiskapiunofficial.tech/api/v2.2/films/top?type=TOP_100_POPULAR_FILMS`, {
    method: 'GET',
    headers: {
      'X-API-KEY': 'd0ee1fcd-c57d-493f-b775-b9af926ea60b',
      'Content-Type': 'application/json',
      },
    })
    .then(res => res.json())
    .then(json => this.films = json.films)
  },
}
</script>

<style>
.container {
    margin: 0 auto;
    max-width: 1368px;
    padding: 0 px;
}
.flex {
  display: flex;
  flex-direction: row;
}
.flex-column {
  display: flex;
  flex-direction: column;
}
button {
  cursor: pointer;
}
* {
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
}
a {
  text-decoration: none;
  font-family: inherit;
}
li {
  list-style-type: none;
  font-family: inherit;
}
</style>
