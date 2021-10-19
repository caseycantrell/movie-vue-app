<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <router-link class="navbar-brand" to="/">Movies</router-link>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNavAltMarkup"
          aria-controls="navbarNavAltMarkup"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
          <div class="navbar-nav">
            <li class="nav-item">
              <router-link class="nav-link" to="/movies">All Movies</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/movies/new">New Movie</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/actors">All Actors</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/actors/new">New Actor</router-link>
            </li>
            <li v-if="!isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/signup">Signup</router-link>
            </li>
            <li v-if="!isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/login">Login</router-link>
            </li>
            <li v-if="isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/logout">Logout</router-link>
            </li>
          </div>
        </div>
      </div>
    </nav>
    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

<script>
export default {
  data: function () {
    return {};
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.jwt;
    },
    getUserId: function () {
      return localStorage.user_id;
    },
  },
};
</script>
