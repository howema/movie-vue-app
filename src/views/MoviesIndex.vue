<template>
  <div class="moviesindex">
    <h1>All Monster Movies:</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <router-link v-bind:to="`/movies/${movie.id}`">
        <div class="card mb-3" style="max-width: 540px">
          <div class="row g-0">
            <div class="col-md-4">
              <v-bind:src="{{movie.image}}" class="img-fluid rounded-start" >
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
      </router-link>
    </div>
  </div>
</template>

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
