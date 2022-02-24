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
  <form>
    <div>
      <h1>Create Movie</h1>
      <p>
        Title:
        <input type="text" id="title" name="newMovie" value="Example Title" required />
      </p>
      <p>
        Year:
        <input type="text" id="year" name="newMovie" value="Example year" required />
      </p>
      <p>
        Plot:
        <input type="text" id="plot" name="newMovie" value="Example plot" required />
      </p>
      <p>
        Director:
        <input type="text" id="director" name="newMovie" value="Example director" required />
      </p>
      <button v-on:click="createMovie()">Create</button>
    </div>
  </form>
</template>

<style>
input:invalid {
  border: 2px dashed red;
}

input:invalid:required {
  background-image: linear-gradient(to right, pink, lightgreen);
}

input:valid {
  border: 2px solid black;
}
</style>
