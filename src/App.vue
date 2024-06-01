<template>
  <div id="app">
    <WeatherTask />
  </div>
</template>

<script>
import WeatherTask from './components/weatherTask.vue'

export default {
  name: 'App',
  components: {
    WeatherTask
  }
}
</script>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
