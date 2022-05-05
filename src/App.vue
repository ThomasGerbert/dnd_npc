<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <GraphCanvas/>
</template>

<script>
import GraphCanvas from './components/GraphCanvas.vue'

export default {
  name: 'App',
  components: {
    GraphCanvas
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
