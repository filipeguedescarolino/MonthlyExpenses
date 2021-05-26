<template>
  <div id="app">
    
    <Costs />
  </div>
</template>

<script>
import Costs from './components/Costs.vue'

export default {
  name: 'App',
  components: {
    Costs
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
