<template>
  <div id="app">
    <div>
      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container-fluid">
          <a class="navbar-brand" href="#">Welcome to Movie Monster</a>
          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <a class="nav-link active" aria-current="page" href="/movies">All Movies</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/">Home</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/about">About</a>
              </li>
              <li class="nav-item"></li>
              <li v-if="!isLoggedIn()">
                <a class="nav-link" href="/signup">Sign-up</a>
              </li>
              <li class="nav-item"></li>
              <li v-if="!isLoggedIn()">
                <a class="nav-link" href="/login">Login</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/movies/new">Add Movie</a>
              </li>
              <li class="nav-item"></li>
              <li v-if="isLoggedIn()">
                <a class="nav-link" href="/logout">Logout</a>
              </li>
              <li v-if="isLoggedIn()">
                <a class="nav-link" href="/actors">Actors</a>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </div>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000000;

}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #50492c;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

body {
  background-image: url("./assets/urban-royalty.gif");
}
</style>

<script>
export default {
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
