<template>
  <div class="movies-index">
    <img src="https://c.tenor.com/OxIKfikF9IsAAAAM/s%C3%B3observo-watchin-movie.gif" />
    <br />
    <br />
    <h1 class="animate__animated animate__lightSpeedInRight animate__slower">All Movies</h1>
    Search by title:
    <input v-model="titleFilter" list="titles" />
    <br />
    <br />

    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>

    <button v-on:click="sortAttribute = 'title'">Sort Alphabetically</button>
    &nbsp;
    <button v-on:click="sortAttribute = 'year'">Sort By Year</button>
    <br />
    <br />
    <div class="container">
      <div class="row row-cols-3">
        <div
          class="col"
          v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), sortAttribute)"
          v-bind:key="movie.id"
        >
          <div class="card" style="width: 18rem">
            <img
              src="https://www.gannett-cdn.com/presto/2020/08/24/PPYD/85a5fe8f-7328-43bf-a7db-da0460ec683d-ENTER-MOVIE-AMC-THEATRES-REOPEN-1-TB.JPG"
              class="card-img-top"
              alt=""
            />
            <div class="card-body">
              <h5 class="card-title">{{ movie.title }}</h5>
              <p class="card-text">Plot: {{ movie.plot }}</p>
              <router-link class="btn btn-primary" :to="`/movies/${movie.id}`">More Details</router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      titleFilter: "",
      sortAttribute: "title",
    };
  },
  created: function () {
    axios.get("/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>
