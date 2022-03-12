<template>
  <div id="app">
    <HeaderComponent
    @get-films="getFilms"
    @send-query="getQuery" 
    @sort-films="sortFilms"
    />

    <FilmsWrapper 
    :query="query"
    :films="films" 
    :page="page"
    :pageIsVisible="pageIsVisible"
    @show-modal="showModal"
    @prev-page="prevPage"
    @next-page="nextPage"
    />

    <ModalFilm 
    :film="this.film"
    ></ModalFilm>
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
      film: {},
      sorted: false,
      page: 1,
      pageIsVisible: true,
    }
  },
  methods: {
    showModal(film) {
      this.film = film
    },
    sortFilms() {
      if (this.sorted) {
        this.films.sort((a, b) => a.rating > b.rating? 1 : -1)
      } else {
        this.films.sort((a, b) => a.rating > b.rating? -1 : 1)
      }
      this.sorted = !this.sorted
    },
    getQuery(query) {
      if (query != "") {
        fetch(`https://kinopoiskapiunofficial.tech/api/v2.1/films/search-by-keyword?keyword=${query}`, {
            method: 'GET',
            headers: {
                'X-API-KEY': '',//Введите свой ключ от Api
                'Content-Type': 'application/json',
            },
        })
        .then(res => res.json())
        .then(json => this.films = json.films)
        this.pageIsVisible = false
      } else {
        alert("Запрос введен некорректно")
      }
      this.sorted = false
    },
    getFilms() {
      fetch(`https://kinopoiskapiunofficial.tech/api/v2.2/films/top?type=TOP_100_POPULAR_FILMS&page=${this.page}`, {
          method: 'GET',
          headers: {
              'X-API-KEY': '', //Введите свой ключ от Api
              'Content-Type': 'application/json',
          },
      })
      .then(res => res.json())
      .then(json => this.films = json.films)
      this.sorted = false
      this.pageIsVisible = true
    },
    nextPage() {
      if (this.page != 16) {
        this.page++
        this.getFilms()
      } else {
        alert("Последняя страница топа")
      }
    },
    prevPage() {
      if (this.page != 1) {
        this.page--
        this.getFilms()
      } else {
        alert("Первая страница топа")
      }
    },
  },
  beforeCreate() {
    fetch(`https://kinopoiskapiunofficial.tech/api/v2.2/films/top?type=TOP_100_POPULAR_FILMS&`, {
    method: 'GET',
    headers: {
      'X-API-KEY': '',
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
