<template>
  <div class="moviesindex">
    <h1>All Monster Movies:</h1>
    <div class="mx-auto" style="width: 500px;">
      Search by title:
      <input v-model="titleFilter" />
      <p></p>
      Search by keyword:
      <input v-model="keywordFilter" />
    <!-- <div v-for="movie in movies" v-bind:key="movie.id"> -->
         <div
          v-for="movie in filterBy(movies, titleFilter, 'title')"
          :key="movie.id"
          >
          <div
          v-for="movie in filterBy(movies, keywordFilter, 'plot')"
          :key="movie.id"
          >
          </div>
      <p></p>

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
                <p>{{ movie.director }}</p>

                <p>
                  <!-- <li v-if="isInEnglish" -->
                  {{ movie.english }}</p>
                <router-link v-bind:to="`/movies/${movie.id}`">
                <small><button type="button" class="btn btn-info">More Info</button></small>
                </router-link>
                <!-- <p></p>
              <p>director: {{ movie.director }}</p> -->
                <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  data: function () {
    return {
      message: "Here are movies",
      movies: [],
      titleFilter: "",
      keywordFilter: "",
    };
  },
  mixins: [Vue2Filters.mixin],
  created: function () {
    this.moviesIndex();
  },
  methods: {
    // isInEnglish: function () {
    //   return this.message("Yes");
    // }
    moviesIndex: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        this.movies = response.data;
        console.log("All movies:", this.movies);
      });
    },
  },
};
</script>

