<template>
  <div id="app">
    <img src="./assets/logo.png">
    <Select></Select>
  </div>
</template>

<script>
import Select from './components/select'

export default {
  name: 'App',
  components: {
    Select
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
