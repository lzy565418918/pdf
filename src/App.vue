<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <home msg="Welcome to scan your PDF"/>
  </div>
</template>

<script>
import home from './pages/home/home.vue'

export default {
  name: 'app',
  components: {
    home
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
