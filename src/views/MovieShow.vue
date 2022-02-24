<script>
import axios from "axios";
export default {
  data: function () {
    return {
      changeMovie: {},
      movie: {},
      currentMovie: {},
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id).then((response) => {
      console.log("movies show", response);
      this.currentMovie = response.data;
    });
  },
  methods: {
    destroyMovie: function () {
      axios.delete("http://localhost:3000/movies/" + this.changeMovie.id).then((response) => console.log(response));
    },
  },
};
</script>
<template>
  <form>
    <div>
      <h1>Update Movie</h1>
      <p>{{ currentMovie }}</p>
      <p>
        Title:
        <input type="text" v-model="changeMovie.title" />
      </p>
      <p>
        Year:
        <input type="text" v-model="changeMovie.year" />
      </p>
      <p>
        Plot:
        <input type="text" v-model="changeMovie.plot" />
      </p>
      <p>
        Director:
        <input type="text" v-model="changeMovie.director" />
      </p>
      <button v-on:click="updateMovie()">Commit</button>
    </div>
    <div>
      <h1>Delete Movie</h1>
      <button v-on:click="destroyMovie()">Delete Movie</button>
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
