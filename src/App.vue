<template>
  <div id="app">
    <div>
      <typeahead :options="options" v-model="selected"></typeahead>
    </div>
  </div>
</template>

<script>
import Typeahead from './components/Typeahead'

export default {
  name: 'app',
  components: {
    Typeahead
  },
  data() {
    return {
      selected: null,
      options: [
        {id: 1, text: 'javascript'},
        {id: 2, text: 'php'},
        {id: 3, text: 'ruby'},
        {id: 4, text: 'goland'},
        {id: 5, text: 'nodejs'}
      ]
    }
  }
}
</script>

<style>
  body {
    font-family: Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin: 60px auto;
    width: 300px;
  }

  * {
    box-sizing: border-box;
    list-style: none;
  }
/*
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
*/
</style>
