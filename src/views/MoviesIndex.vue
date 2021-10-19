<template>
  <div class="movies-index">
    <img src="https://c.tenor.com/OxIKfikF9IsAAAAM/s%C3%B3observo-watchin-movie.gif" />
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
    <div
      is="transition-group"
      appear
      enter-active-class="animate__animated animate__flipInX animate__slow"
      leave-active-class="animate__animated animate__fadeOutRight"
    >
      <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), sortAttribute)" v-bind:key="movie.id">
        <h4>{{ movie.title }}</h4>
        <router-link :to="`/movies/${movie.id}`">See Details</router-link>
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
