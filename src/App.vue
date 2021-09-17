<template>
  <div id="app">
    <img id="logo" alt="Pokemon Logo" src="./assets/Images/PokemonLogo.png">
    <PokemonList msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import PokemonList from './components/PokemonList.vue'

export default {
  name: 'App',
  components: {
    PokemonList,
  }
}
</script>

<style>
@import 'components/style.css';
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
