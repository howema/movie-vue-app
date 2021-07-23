<template>
  <div class="MoviesNew">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newMoviesParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="newMoviesParams.year" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="newMoviesParams.plot" />
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
      errors: [],
      currentMoviesParams: {},
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.currentMoviesParams = response.data;
    });
  },
  methods: {
    updateMovie: function () {
      console.log("Creating movie!");
      axios.patch(`/movies/${this.$route.params.id}`, this.currentMoviesParams.then((response) => {
        console.log(response.data);
        this.$router.push(`/movies/${response.data.id}`);
      });
    },
  },
};
</script>
