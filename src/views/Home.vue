<template>
  <div class="home">
    <div>
      <p></p>
      Title:
      <input type="text" v-model="newMovieParams.title" />
      <p></p>
      Year:
      <input type="text" v-model="newMovieParams.year" />
      <p></p>
      Plot:
      <input type="text" v-model="newMovieParams.plot" />
      <p></p>
      <p></p>
    </div>
    <!-- <button v-on:click="addMovie()">addMovie</button> -->
    <button v-on:click="addMovie()">addMovie</button>
    <div v-for="movie in movies" :key="movie.id">
      <h1>{{ movie.title }}</h1>
      <h2>{{ movie.year }}</h2>
    </div>
  </div>
  <div class="container">
      <h2>{{ movie.title }}</h2>
      <p>{{ movie.year }}</p>
      <img v-bind:src="movie.image" alt="movie.title" />
      <p></p>
      <router-link to="/movies">Back to movies</router-link>
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
      newMovieParams: {},
      movie: {},
    };
  },
  created: function () {
    this.indexMovies();
    axios.get("/movies/" + this.$route.params.id).then((response) => {
      this.movie = response.data;
    });
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        this.movies = response.data;
        console.log("All movies", this.movies);
      });
    },
    createMovie: function () {
      console.log("Added a movie");
      axios
        .post("http://localhost:3000/movies", this.newMovieParams)
        .then((response) => {
          console.log("Nice", response.data);
          this.movies.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
