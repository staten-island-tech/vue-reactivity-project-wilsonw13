<template>
  <div id="app">
    <div class="header">
      <h1 class="header-text">Pizza Generator</h1>
    </div>
    <div class="body">
      <div class="left-container">
        <form id="search-bar" class="search-bar">
          <input type="text" class="search-area" placeholder="Search Toppings"/>
          <input type="button" class="search-button" value="Search"/>
        </form>
        <div class="toppings-container">
          <!-- <img v-for="(object) in responseArray"
            :key="object.id"
            :id="object.id"
            :src="object.src.original + '?auto=compress&cs=tinysrgb&q=75&ar=1:1&fit=crop'"> -->
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
      responseArray: response.photos,
      key: apiKey,
    }
  },
  methods:{

  },
}
</script>

<style>
@import "./css/style.css";
</style>
