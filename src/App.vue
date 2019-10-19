<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <NGOs />
  </div>
</template>

<script>
import NGOs from './components/NGOs.vue'

export default {
  name: 'app',
  components: {
    NGOs
  },
  rules: {
        'no-console': 'off',
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
