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
          <img v-for="(object) in responseArray"
            :key="object.id"
            :src="object.urls.raw + '&q=75&ar=1:1&fit=crop'" :alt="object.description">
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

export default {
  name: 'App',
  components: {
  },
  data(){
    return{
      responseArray: response.results,
    }
  },
}
</script>

<style>
:root {
  --navy-blue: #243156;
  --gray: #6B7B95;
  --light-blue: #A4BBCC;
  --white: #fff;
  --pink: #E2B4BD;
  --copper: #936264;
  --burgundy: #9A5B62;
  --website-bg: var(--pink);
  --search-button: var(--burgundy);
  --h1: 6rem;
  --input: 3rem;
  --p: 3rem;
  --containerPadding: 2.5%;
  --headerHeight: 3rem;
  --borderRadius: 10px;
  --primaryFont: "Lato", sans-serif;
  --secondaryFont: "Playfair Display", serif;

  /* Measurements */
}


*, html {
  box-sizing: border-box;
  font-size: 62.5%;
  font-weight: 400;
  margin: 0;
  padding: 0;
}

#app {
  height: 100%;
  width: 100%;
}

body {
  background-color: var(--website-bg);
}

h1 {
  font-family: var(--primaryFont);
  font-size: var(--h1);
}

p {
  font-family: var(--secondaryFont);
  font-size: var(--p);
}

.header {
  width: 100%;
  margin: 1.5rem 0;
}

.header-text {
  text-align: center;
}

.body {
  height: 80rem;
  width: 100%;

  display: flex;
  justify-content: space-evenly;
  align-items: center;

/*   background-color: green; */
}

.body > div {
  height: 100%;
  width: 45%;
}

.left-container {
  background-color: rgba(0, 0, 256, 0.25);

  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
}

.search-bar {
  height: 8rem;
  width: 100%;
  position: relative;
  margin: 2rem auto;

  display: flex;
  justify-content: space-evenly;
  align-items: center;
}

.search-bar input {
  height: 70%;
  margin: 0rem 0.5rem;
  font-size: var(--input);
  font-family: var(--secondaryFont);
}

.search-area {
  width: 35vw;
  min-width: 28rem;
  padding: 0rem 1rem 0rem 4.8rem;
  border-radius: 1rem;

  /* Format Magnifying Glass Icon */

  background-image: url(assets/search-icon.png);
  background-size: 2.3rem;
  background-repeat: no-repeat;
  background-position: 1.1rem center;
}

.search-area:focus {
  border: 0.2rem solid var(--burgundy);
}

.search-button {
  width: 7vw;
  min-width: 12rem;
  max-width: 20rem;
  
  background: none;
  background-color: var(--search-button);
  color: var(--white);
  /* transition: all 0.3s;
  border: 0.3rem double color(light-gray); */
  cursor: pointer;
}

.toppings-container {
  height: 80%;
  width: 100%;

  display: flex;
  align-content: flex-start;
  justify-content: space-evenly;
  flex-wrap: wrap;
}

.toppings-container > img {
  width: 27%;
  margin: 1.5rem;
  cursor: pointer;
}

.right-container {
  background-color: rgba(256, 0, 0, 0.25);
}
</style>
