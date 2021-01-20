<template>
  <div id="app">
    <div v-for="(pokemon, index) in pokemons" :key="index">
      <Pokemon  :number="index + 1" :name="pokemon.name"/>
    </div>
  </div>
</template>

<script>
import api from "./services/api";

import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  created: function() {
    api.get('pokemon?limit=151&offset=0').then(response => {
      this.pokemons = response.data.results;
    });
  },
  data() {
    return {
      pokemons: []
    }
  },
  components: {
    Pokemon
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

  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;

  gap: 1.5rem;

  padding: 2rem;
}
</style>
