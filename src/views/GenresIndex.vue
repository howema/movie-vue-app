<template>
  <div class="genresindex">
    <h1>All Monster Genres:</h1>
    <div class="mx-auto" style="width: 500px">
      Search by genre:
      <input v-model="titleFilter" />
      <p></p>
      <div v-for="genre in filterBy(genres, titleFilter, 'name')" :key="genre.id">
        <p></p>

        <div class="card mb-3" style="max-width: 540px">
          <div class="row g-0">
            <div class="col-md-4">
              <!-- <v-bind:src="{{genre.image}}" class="img-fluid rounded-start" > -->
            </div>

            <div class="col-md-8">
              <div class="card-body">
                <h5 class="card-title">{{ genre.name }}</h5>
                <p class="card-text">
                  <!-- <li v-if="isInEnglish" -->
                  {{ genre.english }}
                </p>
                <router-link v-bind:to="`/genres/${genre.id}`">
                  <small><button type="button" class="btn btn-info">See Movies</button></small>
                </router-link>
                <!-- <p></p>
              <p>director: {{ genre.director }}</p> -->
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
      message: "Here are genres",
      genres: [],
      titleFilter: "",
      keywordFilter: "",
    };
  },
  mixins: [Vue2Filters.mixin],
  created: function () {
    this.genresIndex();
  },
  methods: {
    // isInEnglish: function () {
    //   return this.message("Yes");
    // }
    genresIndex: function () {
      axios.get("http://localhost:3000/genres").then((response) => {
        this.genres = response.data;
        console.log("All genres:", this.genres);
      });
    },
  },
};
</script>
