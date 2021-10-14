<template>
  <div id="app">
    <div class="header-textbox">
      <h1 class="header">Pizza Generator</h1>
    </div>
    <form id="search-form" class="search-form">
      <input
        type="text"
        class="search-area"
        placeholder="Search Toppings ..."
      />
      <input type="button" class="search-button" value="Search"/>
    </form>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
  }
}
</script>

<style>
:root {
  --black: #131313;
  --light-black: #232323;
  --white: #fff;
  --off-white: #f0f1f6;
  --dark-grey: #1a2f41;
  --grey: #252c30;
  --lightGrey: #f2f4f6;
  --background-primary: var(--light-black);
  --skill-background: var(--black);
  --card-background: var(--light-black);
  --card-text: var(--white);
  --background-secondary: var(--dark-grey);
  --text-primary: var(--white);
  --text-secondary: var(--black);
  --modal-background: var(--black);
  --modal-text: var(--white);
  --student-text: var(--white);
  --link-text: var(--white);
  --nav-line: var(--white);
  --header-btn: var(--white);
  --h1: 8rem;
  --h2: 5rem;
  --containerPadding: 2.5%;
  --headerHeight: 3rem;
  --borderRadius: 10px;
  --primaryFont: "Lato", sans-serif;
  --secondaryFont: "Playfair Display", serif;
}
html {
  box-sizing: border-box;
  font-size: 62.5%;
  font-weight: 400;
}

h1 {
  font-family: var(--secondaryFont);
}
</style>
