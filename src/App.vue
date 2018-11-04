<template>
  <div id="app">
    <concentration />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Concentration from './components/concentration'

export default {
  name: 'App',
  components: {
    Concentration
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: -50px;
}
</style>
