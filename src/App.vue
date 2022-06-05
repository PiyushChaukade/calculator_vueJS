<template>

<calculator-main></calculator-main>

</template>

<script>
import calculatorMain from './components/calculatorMain.vue'
export default {
  name: 'App',
  components: {
    calculatorMain
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
