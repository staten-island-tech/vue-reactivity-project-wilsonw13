<template>
  <div id="app">
    <div class="header">
      <h1 class="header-text">Pizza Generator</h1>
    </div>
    <div class="body">
      <div class="left-container">
        <form
          id="search-bar"
          class="search-bar"
          @submit.prevent="getSearchData(searchQuery)"
        >
          <input
            type="text"
            class="search-area"
            placeholder="Search Toppings"
            v-model="searchQuery"
          />
          <input type="submit" class="search-button" value="Search"/>
        </form>
        <div class="toppings-container">
          <img
            v-for="object in currentResponseArray"
            :key="object.id"
            :src="object.src.original + '?auto=compress&cs=tinysrgb&q=75&ar=1:1&fit=crop'"
            @click="changeClickedTopping($event, object)"
            class="topping-image"
          />
        </div>
      </div>
      <div class="right-container">
        <div class="pizza-container" @click="imageOnPizza($event)">
          <img
            class="pizza"
            src="./assets/no-toppings-pizza.png"
            alt="pizza"
          />
          <div class="pizza-image-container">
            <img class="pizza-images"
            v-for="(object, index) in pizzaArray"
            :key="object.imageObject.id + '-' + index"
            :src="object.imageObject.src.original + '?auto=compress&cs=tinysrgb&q=75&ar=1:1&fit=crop'"
            :style="object.style"
            >
          </div>
        </div>
        <div class="history-container">
          <img
            class="topping-image"
            v-for="object in historyArray"
            :key="object.id"
            :src="object.src.original + '?auto=compress&cs=tinysrgb&q=75&ar=1:1&fit=crop'"
            @click="changeClickedTopping($event, object)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import response from "./assets/response.json";

export default {
  name: "App",
  data() {
    return {
      sampleResponseArray: response.photos,

      searchQuery: null,
      previousQuery: null,
      apiRequestsRemaining: null,
      apiHeaders: null,

      apiResponseArray: null,
      historyArray: [],
      pizzaArray: [],

      currentToppingObject: null,

      pexelsApiKey: process.env.VUE_APP_PEXELS_API_KEY,
    };
  },
  methods: {
    async getSearchData(query = "pepperoni", page = 1) {
      switch (query) {
        case this.previousQuery:
          console.log("Error: Same thing was searched");
          return;
        case "pineapple":
          console.log("Error: PINEAPPLE IS NOT A VALID TOPPING!");
          return;
        case "":
          console.log("Error: Nothing was searched");
          return;
      }
      try {
        const response = await fetch(
          `https://api.pexels.com/v1/search?query=${query}&page=${page}&per_page=12`,
          {
            mode: "no-cors",
            headers: { Authorization: this.pexelsApiKey },
          }
        );
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
    imageOnPizza(event, currentToppingObj = this.currentToppingObject) {
      // elRect = the properties of the (rectangle) element
      // X is from left, Y is from top
      const elRect = event.currentTarget.getBoundingClientRect();
      const pixelsX = event.clientX - elRect.left;
      const pixelsY = event.clientY - elRect.top;

      const percentX = Math.round((pixelsX * 100) / elRect.width);
      const percentY = Math.round((pixelsY * 100) / elRect.height);

      let isDuplicateImage = false;

      // tests if the current topping is already in history array
      this.historyArray.forEach((obj) => {
        if (obj === currentToppingObj) {
          isDuplicateImage = true;
        }
      });

      if (currentToppingObj != null) {
        if (!isDuplicateImage) {
          // Unshift adds the element to the beginning of the array
          this.historyArray.unshift(currentToppingObj);
        }

        this.pizzaArray.push({
          style: {
            left: `${percentX}%`,
            top: `${percentY}%`,
          },
          imageObject: currentToppingObj,
        });
      }
    },
    changeClickedTopping(event, toppingObject) {
      const selectedToppingsHTML = document.querySelectorAll(
        ".topping-selected"
      );

      selectedToppingsHTML.forEach((e) =>
        e.classList.remove("topping-selected")
      );

      event.target.classList.add("topping-selected");
      this.currentToppingObject = toppingObject;
    },
  },
  computed: {
    // If there has been no previous query, return a sample array. Otherwise, return new array from API.
    currentResponseArray() {
      if (!this.previousQuery) return this.sampleResponseArray;
      else return this.apiResponseArray;
    },
  },
};

</script>

<style>
@import "./css/main.css";
</style>