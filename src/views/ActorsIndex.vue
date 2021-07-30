<template>
  <div class="actorsindex">
    <h1>All Monster actors:</h1>
    <div class="mx-auto" style="width: 500px;">
      Search by name:
      <input v-model="nameFilter" />
      <p></p>
         <div
          v-for="actor in filterBy(actors, nameFilter, 'first_name', 'last_name')"
          :key="actor.id"
          >

      <p></p>

        <div class="card mb-3" style="max-width: 540px">
          <div class="row g-0">
            <div class="col-md-4">
              <v-bind:src="{{actor.image}}" class="img-fluid rounded-start" >
            </div>
            <div class="col-md-8">
              <div class="card-body">
                <h5 class="card-title">{{ actor.first_name }} {{ actor.last_name }}</h5>
                <p class="card-text">
                
                <p>Age: {{ actor.age }}</p>
                <p>Gender: {{ actor.gender }}</p>
                <p>Known For: {{ actor.known_for }}</p>
                <router-link v-bind:to="`/actors/${actor.id}`">
                <small><button type="button" class="btn btn-info">More Info</button></small>
                </router-link>
                <!-- <p></p>
              <p>director: {{ actor.director }}</p> -->
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
      message: "Here are actors",
      actors: [],
      nameFilter: "",
      keywordFilter: "",
    };
  },
  mixins: [Vue2Filters.mixin],
  created: function () {
    this.actorsIndex();
  },
  methods: {
    actorsIndex: function () {
      axios.get("http://localhost:3000/actors").then((response) => {
        this.actors = response.data;
        console.log("All actors:", this.actors);
      });
    },
  },
};
</script>

