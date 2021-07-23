<template>
  <div class="moviesindex">
    <h1>Here Come the movies!</h1>
    <router-link to="/movies/10">Check out this gator</router-link>
    <div v-for="movie in movies" :key="movie.id">
      <router-link v-bind:to="`/movies/${movie.id}`">
        <h2>{{ movie.title }}</h2>
        <p>{{ movie.body }}</p>
        <img v-bind:src="movie.image" alt="movie.title" />
      </router-link>
      <!-- <p></p> -->
      <!-- <button>Buttonz!</button> -->
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Here are movies",
      movies: [],
    };
  },
  created: function () {
    this.moviesIndex();
  },
  methods: {
    moviesIndex: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        this.movies = response.data;
        console.log("All movies:", this.movies);
      });
    },
  },
};
</script>
