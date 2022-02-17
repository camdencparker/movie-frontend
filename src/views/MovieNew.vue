<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newMovie: {},
      movies: [],
    };
  },
  methods: {
    createMovie: function () {
      axios
        .post("http://localhost:3000/movies", this.newMovie)
        .then((response) => {
          console.log("movie create", response);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log("movie create error", error.response);
          this.errors = error.response.data.errors;
        });
      this.newMovie = {};
    },
  },
};
</script>
<template>
  <div>
    <h1>Create Movie</h1>
    <p>
      Title:
      <input type="text" v-model="newMovie.title" />
    </p>
    <p>
      Year:
      <input type="text" v-model="newMovie.year" />
    </p>
    <p>
      Plot:
      <input type="text" v-model="newMovie.plot" />
    </p>
    <p>
      Director:
      <input type="text" v-model="newMovie.director" />
    </p>
    <p>
      Is English:
      <input type="text" v-model="newMovie.english" />
    </p>
    <button v-on:click="createMovie()">Create</button>
  </div>
</template>