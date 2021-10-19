<template>
  <div class="movies-new">
    <img src="https://i.kym-cdn.com/photos/images/newsfeed/000/673/870/899.gif" />
    <form v-on:submit.prevent="createMovie()">
      <label for="New Movie"><h1>New Movie</h1></label>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label for="Title">Title:&nbsp;</label>
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <br />
      <div>
        <label for="Year">Year:&nbsp;</label>
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <br />
      <div>
        <label for="Plot">Plot:&nbsp;</label>
        <input type="text" v-model="newMovieParams.plot" />
      </div>
      <div>
        <br />
        <form action="/action_page.php">
          <label for="favcolor">What's your favorite color, dude?&nbsp;</label>
          <input type="color" id="favcolor" name="favcolor" value="#ff0000" />
        </form>
      </div>
      <br />
      <input class="btn btn-primary mb-3" type="submit" value="Create" />
      &nbsp;
      <input class="btn btn-secondary mb-3" type="reset" value="Reset" />
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
