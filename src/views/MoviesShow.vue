<template>
  <div class="moviesshow">
    <div class="container">
      <h1>{{ movie.title }} ({{ movie.year }})</h1>
      <h2>{{  }}</h2>
      <p>{{ movie.plot }}</p>
      <p>Directed by: {{ movie.director }}</p>
      <p>Is it in English? {{ movie.english }}</p>
      <p>{{ movie.image }}</p>
      <!-- <p>{{ movie.actor.first_name }}</p> -->
      <!-- <img v-bind:src="movie.image" alt="movie.title" /> -->
      <p></p>
      <router-link v-bind:to="`/movies/${movie.id}/edit`"><button>Edit movie</button></router-link>
      <p></p>
      <router-link to="/movies">Back to movies</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      errors: [],
      movie: {},
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id).then((response) => {
      this.movie = response.data;
      console.log(response.data);
    });
  },
};
</script>
