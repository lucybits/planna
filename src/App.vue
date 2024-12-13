<template>
  <div id="app">
    <HomeView /> 
  </div>
</template>

<script>
import HomeView from './views/HomeView.vue'

export default {
  name: 'App',
  components: {
    HomeView
  }
}
</script>

<style>
* {
  font-family: 'Plus Jakarta Sans', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #1a1a2e;
  margin: 0;
  padding: 0;
}
</style>
