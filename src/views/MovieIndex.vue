<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
      titleFilter: "",
    };
  },
  created: function () {
    this.indexMovies();
  },
  computed: {
    filterMovies: function () {
      return this.movies.filter((movie) => {
        return movie.title.toLowerCase().includes(this.titleFilter.toLowerCase());
      });
    },
  },
  methods: {
    indexMovies: function () {
      axios.get("/movies").then((response) => {
        console.log("movies index", response);
        this.movies = response.data;
      });
    },
  },
};
</script>

<template>
  <div class="movies-index">
    <h1>All Movies</h1>
    <p>
      Search by title
      <input v-model="titlefilter" />
    </p>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>{{ movie.title }}</h2>
      <p>
        <b>Year:</b>
        <b>{{ movie.year }}</b>
      </p>
      <p>
        <b>Plot:</b>
        {{ movie.plot }}
      </p>
      <router-link v-bind:to="`/movies/${movie.id}`">More details</router-link>
      <br />
      <em>Have You Seen This Film? if so check the box</em>
      <input type="checkbox" />
    </div>
  </div>
</template>
