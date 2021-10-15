<template>
  <div class="hello">
    <h1>{{ msg + "testing testing 1, 2, 3"}}</h1>
  </div>
</template>

<script>
export default {
  name: 'ToppingImage',
  props: {
    msg: String
  },
  data() {
    return {
      content: "test",
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
