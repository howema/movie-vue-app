<template>
  <div class="moviesedit">
    <form v-on:submit.prevent="updateMovie()">
      <h1>New Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="currentMoviesParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="currentMoviesParams.year" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="currentMoviesParams.plot" />
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
      newMoviesParams: {},
    };
  },
  methods: {
    createMovie: function () {
      console.log("Creating movie!");
      axios.post("/movies", this.newMoviesParams).then((response) => {
        this.$router.push("/movies");
        console.log(response.data);
      });
    },
  },
};
</script>
