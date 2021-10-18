<template>
  <div id="app">
    <div class="header">
      <h1 class="header-text">Pizza Generator</h1>
    </div>
    <div class="body">
      <div class="left-container">
        <form id="search-bar" class="search-bar">
          <input type="text" class="search-area" placeholder="Search Toppings" v-model="searchQuery"/>
          <input type="button" class="search-button" value="Search" @click="getSearchData(searchQuery)"/>
        </form>
        <div class="toppings-container">
          <img v-for="object in currentResponseArray"
            :key="object.id"
            :src="object.src.original + '?auto=compress&cs=tinysrgb&q=75&ar=1:1&fit=crop'">
        </div>
      </div>
      <div class="right-container">
        <div class="pizza-container" @click="getClickPosition($event)"></div>
        <div class="history-container"></div>
      </div>
    </div>
  </div>
</template>

<script>
import response from "./assets/response.json"
import apiKey from "./assets/apiKey.js"

export default {
  name: 'App',
  data(){
    return{
      sampleResponseArray: response.photos,

      searchQuery: null,
      previousQuery: null,
      apiResponseArray: null,

      apiRequestsRemaining: null,
      apiHeaders: null,

    }
  },
  methods:{
    async getSearchData (query = "pepperoni", page = 1) {   
      switch (query) {
        case this.previousQuery:
          console.log("Error: Same thing was searched");
          return;
        case "pineapple":
          console.log("Error: PINEAPPLE IS NOT A VALID TOPPING!");
          return;
        case "":
          console.log("Error: Nothing was searched")
          return;
      }
      try {
        const response = await fetch(`https://api.pexels.com/v1/search?query=${query}&page=${page}&per_page=12`, {
          headers: {"Authorization": apiKey},
        });
        const DataJSON = await response.json();

        if (!DataJSON.photos.length) return;
        this.apiResponseArray = DataJSON.photos;
        this.previousQuery = query;

        /* for (const pair of response.headers.entries()) {
          if (pair[0] === "x-total-count") {}
        }
        this.apiHeaders = response.headers.entries();
        console.log(this.apiHeaders); */

      } catch (error) {
        console.log(error);
        // alert("Great Error Handling :D - An error as occured!");
      }
    },
    getClickPosition(event) {
      // elRect = the properties of the (rectangle) div element
      const elRect = event.target.getBoundingClientRect();
      const pixelsX = event.clientX - elRect.left;
      const pixelsY = event.clientY - elRect.top;

      const percentX = Math.round(pixelsX * 100 / elRect.width);
      const percentY = Math.round(pixelsY * 100 / elRect.height);

      console.log(`Current Position: (${percentX}%, ${percentY}%)`);
    }
  },
  computed: {
    // If there has been no previous query, return a sample array. Otherwise, return new array from API.
    currentResponseArray() {
      if (!this.previousQuery) return this.sampleResponseArray;
      else return this.apiResponseArray;
    }
  }
}
</script>

<style>
@import "./css/style.css";
</style>
