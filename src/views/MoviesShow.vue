<template>
  <div class="movies-show">
    <h2>{{ movie.title }}</h2>
    <p>Year: {{ movie.year }}</p>
    <p>Plot: {{ movie.plot }}</p>
    <p>Director: {{ movie.director }}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {},
};
</script>
