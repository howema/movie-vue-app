<template>
  <div class="MoviesNew">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="newMovieParams.plot" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newMovieParams: { english: false },
      errors: [],
    };
  },
  methods: {
    newMovie: function () {
      console.log(this.newMovieParams);
      axios.post("http://localhost:3000/movies", this.newMovieParams).then((response) => {
        console.log(response.data, response.errors);
      });
    },
  },
};
</script>
