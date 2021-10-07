<template>
  <div class="actors-index">
    <h1>All Actors</h1>
    <div v-for="actor in actors" v-bind:key="actor.id">
      <h3>{{ actor.first_name }} {{ actor.last_name }}</h3>
      <p>Age: {{ actor.age }}</p>
      <p>Known For: {{ actor.known_for }}</p>
      <router-link :to="`/actors/${actor.id}`">See Details</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      actors: [],
    };
  },
  created: function () {
    axios.get("/actors").then((response) => {
      console.log(response.data);
      this.actors = response.data;
    });
  },
  methods: {},
};
</script>
