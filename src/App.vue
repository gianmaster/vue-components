<template>
  <div id="app">
    <img src="./assets/logo.png">
    <div>
      <typeahead></typeahead>
    </div>
  </div>
</template>

<script>
import Typeahead from './components/Typeahead'

export default {
  name: 'app',
  components: {
    Typeahead
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
