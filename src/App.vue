<template>
  <div id="app">
    <SchulteGrid/>
  </div>
</template>

<script>
import SchulteGrid from './components/SchulteGrid'

export default {
  name: 'app',
  components: {
    SchulteGrid
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
