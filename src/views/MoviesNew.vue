<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:&nbsp;</label>
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <br />
      <div>
        <label>Year:&nbsp;</label>
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <br />
      <div>
        <label>Plot:&nbsp;</label>
        <input type="text" v-model="newMovieParams.plot" />
      </div>
      <br />
      <input type="submit" value="Create" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newMovieParams: {},
      errors: [],
    };
  },
  methods: {
    createMovie: function () {
      axios
        .post("/movies", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
          window.alert("New movie successfully created!");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
