<template>
  <div class="home">
    <h1>New Movie</h1>
    <div>
      Title:
      <input type="text" v-model="newMovieParams.title" />
    </div>
    <div>
      Year:
      <input type="text" v-model="newMovieParams.year" />
    </div>
    <div>
      Director:
      <input type="text" v-model="newMovieParams.director" />
    </div>
    <div>
      Plot:
      <input type="text" v-model="newMovieParams.plot" />
    </div>
    <p>Movie Params: {{ newMovieParams }}</p>
    <button v-on:click="createMovie()">Create New Movie</button>
    <br />
    <h1>Cool Movies:</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <p>Title: {{ movie.title }}</p>
      <p>Year: {{ movie.year }}</p>
      <p>Director: {{ movie.director }}</p>
      <p>Plot: {{ movie.plot }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
      newMovieParams: {},
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
        .post("http://localhost:3000/movies", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.movies.push(response.data);
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
