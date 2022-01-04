<template>
  <div id="app">
    <flight/>
  </div>
</template>

<script>
import flight from './components/flight'

export default {
  name: 'App',
  components: {
    flight
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
