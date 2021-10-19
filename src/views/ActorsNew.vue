<template>
  <div class="actors-new">
    <form v-on:submit.prevent="createActor()">
      <h1>New Actor</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>First Name:</label>
        <input type="text" v-model="newActorParams.first_name" />
      </div>
      <div>
        <label>Last Name:</label>
        <input type="text" v-model="newActorParams.last_name" />
      </div>
      <div>
        <label>Age:</label>
        <input type="text" v-model="newActorParams.age" />
      </div>
      <div>
        <label>Known For:</label>
        <input type="text" v-model="newActorParams.known_for" />
      </div>
      <br />
      <input class="btn btn-info mb-3" type="submit" value="Create Actor" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newActorParams: {},
      errors: [],
    };
  },
  methods: {
    createActor: function () {
      axios
        .post("/actors", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/actors");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
