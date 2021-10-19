<template>
  <div class="actors-show">
    <h2>{{ actor.first_name }} {{ actor.last_name }}</h2>
    <p>Age: {{ actor.age }}</p>
    <p>Known For: {{ actor.known_for }}</p>
    <router-link :to="`/actors/${actor.id}/edit`">Edit</router-link>
    <br />
    <br />
    <button class="btn btn-danger btn-lg" v-on:click="destroyActor()">Delete</button>
    <br />
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      actor: {},
    };
  },
  created: function () {
    axios.get(`/actors/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.actor = response.data;
    });
  },
  methods: {
    destroyActor: function () {
      if (confirm("Are you sure you want to delete this actor?")) {
        axios.delete(`/actors/${this.actor.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/actors");
          window.alert("Actor successfully deleted!");
        });
      }
    },
  },
};
</script>
