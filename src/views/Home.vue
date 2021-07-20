<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <button v-on:click="addMovie()">addMovie</button>
    <div v-for="movie in movies" :key="movie.id">
      <h1>{{ movie.name }}</h1>
      <h2>{{ movie.year }}</h2>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        this.movies = response.data;
        console.log("All movies", this.movies);
      });
    },
    addMovie: function () {
      console.log("Add a movie");

      var params = {
        name: "The Count of Monte Cristo",
        year: 1692,
      };
      axios.post("http://localhost:3000/movies", params).then((response) => {
        console.log("Nice", response.data);
        this.products.push(response.data);
      });
    },
  }
};
</script>
