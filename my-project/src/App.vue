<template>
  <div id="app">
    <img src="./assets/logo.png">
    <getPdfContent fn="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import getPdfContent from './components/getPdfContent.vue'

export default {
  name: 'app',
  components: {
    getPdfContent
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
