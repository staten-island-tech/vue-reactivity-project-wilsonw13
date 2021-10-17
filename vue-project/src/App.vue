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
          <img v-for="object in responseArray"
            :key="object.id"
            :src="object.src.original + '?auto=compress&cs=tinysrgb&q=75&ar=1:1&fit=crop'">
        </div>
      </div>
      <div class="right-container">
        <div class="pizza-pie"></div>
      </div>
    </div>
  </div>
</template>

<script>
import response from "./assets/response.json"
import apiKey from "./assets/apiKey.js"

export default {
  name: 'App',
  components: {
  },
  data(){
    return{
      searchQuery: null,
      previousQuery: null,
      responseArray: null,
      sampleResponse: response.photos,

    }
  },
  methods:{
    async getSearchData (query = "pepperoni") {
      if (query === this.previousQuery) {
        console.log("Don't type the same thing!");
        return;
      }
      try {
        const response = await fetch(`https://api.pexels.com/v1/search?query=${query}&per_page=12`, {
          headers: {"Authorization": apiKey},
        });
        const DataJSON = await response.json();
        this.responseArray = DataJSON.photos;
        this.previousQuery = query;
      } catch (error) {
        console.log(error);
        // alert("Great Error Handling :D - An error as occured!");
      }
    },
  },
}
</script>

<style>
@import "./css/style.css";
</style>
