<template>
  <div id="app">
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
  --footer-icon: var(--light-black);
  --h1: 7.594rem;
  --h2: 5.063rem;
  --h3: 3.375rem;
  --h4: 2.25rem;
  --h5: 1.5rem;
  --smallText: 0.8rem;
  --containerPadding: 2.5%;
  --headerHeight: 3rem;
  --borderRadius: 10px
}
html {
  box-sizing: border-box;
  font-size: 62.5%;
}

#app {
  font-weight: 400;
  line-height: 1.75;
  background-color: var(--background-primary);
  color: var(--text-primary);
  margin: 0;
  font-family: "Crimson Text",serif
}
</style>
