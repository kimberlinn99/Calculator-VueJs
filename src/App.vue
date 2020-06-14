<template>
  <div id="app">
    <Header />
    <Calculator />
    <Warning />
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'
import Header from './components/Header.vue'
import Warning from './components/Warning.vue'

export default {
  name: 'App',
  components: {
    Calculator,
    Header,
    Warning
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
}
</style>
