<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <CalculadoraComponente msg="Calculadora"/>
</template>

<script>
import CalculadoraComponente from './components/CalculadoraComponente.vue'

export default {
  name: 'App',
  components: {
    CalculadoraComponente
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
