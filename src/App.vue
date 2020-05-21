<template>
  <div id="app">
    <Fuzzy/>
  </div>
</template>

<script>
import Fuzzy from './components/Fuzzy.vue'

export default {
  name: 'app',
  components: {
    Fuzzy
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
