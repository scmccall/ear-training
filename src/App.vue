<template>
  <div id="app">
    <Intervals/>
  </div>
</template>

<script>
import Intervals from './components/Intervals.vue'

export default {
  name: 'App',
  components: {
    Intervals
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
