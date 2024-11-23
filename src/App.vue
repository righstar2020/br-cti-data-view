<template>
  <div id="app">
    <DataView></DataView>
  </div>
</template>

<script>
import DataView from './components/DataView.vue'
export default {
  name: 'App',
  components: {
    DataView
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
