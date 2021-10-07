<template>
  <div class="actors-edit">
    <form v-on:submit.prevent="updateActor()">
      <h1>Edit Actor</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>First Name:</label>
        <input type="text" v-model="editActorParams.first_name" />
      </div>
      <div>
        <label>Last Name:</label>
        <input type="text" v-model="editActorParams.last_name" />
      </div>
      <div>
        <label>Age:</label>
        <input type="text" v-model="editActorParams.age" />
      </div>
      <div>
        <label>Known For:</label>
        <input type="text" v-model="editActorParams.known_for" />
      </div>
      <br />
      <input type="submit" value="Update" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      editActorParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/actors/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.editActorParams = response.data;
    });
  },
  methods: {
    updateActor: function () {
      axios
        .patch(`/actors/${this.editActorParams.id}`, this.editActorParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/actors/${response.data.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
