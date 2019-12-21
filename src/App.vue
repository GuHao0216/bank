<template>
  <div id="app">
<!--    <img alt="Vue logo" src="./assets/logo.png">-->
    <Bank></Bank>
  </div>
</template>

<script>
import Bank from './components/bank.vue'

export default {
  name: 'app',
  components: {
    Bank
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
