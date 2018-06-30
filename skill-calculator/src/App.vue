<template>
  <div id="app">
    <img src="./assets/logo.png">
    <Questionary students = "45"/>
   <!--<HelloWorld msg="Welcome to Your Vue.js App"/>-->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Questionary from './components/Questionary.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Questionary
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
