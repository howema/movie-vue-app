<template>
  <div class="moviesindex">
    <h1>All Monster Movies:</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <div class="card mb-3" style="max-width: 540px">
        <div class="row g-0">
          <div class="col-md-4">
            <img src="actor.png" class="img-fluid rounded-start" alt="card image capppp" />
          </div>
          <div class="col-md-8">
            <div class="card-body">
              <h5 class="card-title">{{ movie.title }} ({{ movie.year }})</h5>
              <p class="card-text">
              {{ movie.plot }}
              </p>
              <!-- <p></p>
              <p>director: {{ movie.director }}</p> -->
              <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <p></p>
    <p></p>
    <p></p>
    <!-- <router-link to="/movies/16">Check out this movie</router-link> -->
    <div v-for="movie in movies" v-bind:key="movie.id">
      <router-link v-bind:to="`/movies/${movie.id}`">
        <h2>{{ movie.title }}</h2>
        <p>{{ movie.plot }}</p>
        <!-- <img v-bind:src="movie.image" alt="movie.title" /> -->
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
