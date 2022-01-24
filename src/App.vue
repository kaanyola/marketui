<template>
  <div id="app">
    <ListingPage />
  </div>
</template>

<script>
import ListingPage from './views/ListingPage.vue'

export default {
  name: 'App',
  components: {
    ListingPage
  }
}
</script>

<style>
#app {
  display: flex;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  align-items: center;
  justify-content: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
