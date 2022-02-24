<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to the Cinema",
      movies: [],
      newMovie: {},
      changeMovie: {},
      showDirector: false,
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function () {
      axios
        .post("http://localhost:3000/movies", this.newMovie)
        .then((response) => this.movies.unshift(response.data))
        .catch((error) => {
          console.log(error.response);
        });
      this.newMovie = {};
    },
    updateMovie: function () {
      this.params = {
        title: this.changeMovie.title,
        director: this.changeMovie.director,
        year: this.changeMovie.year,
        plot: this.changeMovie.plot,
      };
      axios
        .patch("http://localhost:3000/movies/" + this.changeMovie.id, this.params)
        .then((response) => console.log(response.data))
        .catch((error) => console.log(error.response));
    },
    destroyMovie: function () {
      axios.delete("http://localhost:3000/movies/" + this.changeMovie.id).then((response) => console.log(response));
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
  </div>
</template>

<style>
p {
  background-image: url("/rick.jpg");
}
</style>
