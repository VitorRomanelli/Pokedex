<template>
  <div id="app">
    <div class="header">
      <img src="./assets/logo.png" alt="Pokemon Logo" />
      <span> Pokedex </span>
      <input
        type="text"
        placeholder="Search"
        v-model="search"
        id="search-input"
      />
      <button @click="searchPokemon">Search</button>
    </div>
    <div class="pokemons">
      <div v-for="(pokemon, index) in filter" :key="pokemon.url">
        <Pokemon :number="index + 1" :name="pokemon.name" :url="pokemon.url" />
      </div>
    </div>
  </div>
</template>

<script>
import api from "./services/api";

import Pokemon from "./components/Pokemon";

export default {
  name: "App",
  created: function () {
    api.get("pokemon?limit=151&offset=0").then((response) => {
      this.pokemons = response.data.results;
      this.filter = response.data.results;
    });
  },
  data() {
    return {
      search: "",
      pokemons: [],
      filter: [],
    };
  },
  components: {
    Pokemon,
  },
  methods: {
    searchPokemon: function () {
      this.filter = this.pokemons;
      if (this.search === "" || this.search === " ") {
        this.filter = this.pokemons;
      } else {
        this.filter = this.pokemons.filter(
          (pokemon) => pokemon.name.toLowerCase() === this.search.toLowerCase()
        );
        console.log(this.filter);
      }
    },
  },
  computed: {
    searchResult: function () {
      if (this.search === "" || this.search === " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter(
          (pokemon) => pokemon.name.toLowerCase() === this.search.toLowerCase()
        );
      }
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Lobster&display=swap");

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.header {
  display: flex;
  flex-direction: column;
  align-items: center;

  width: 100%;
  height: 240px;

  box-sizing: border-box;
}

img {
  width: 13%;
}

#search-input {
  margin: 10px;
  width: 40%;
  height: 2rem;

  border: none;
  border-radius: 8px;

  box-shadow: 0 0 0.8em #0004;
  padding-left: 1.5rem;

  outline: none;
}

#search-input:focus {
  outline: 2px auto #ecd825;
  box-shadow: none;
}

span {
  margin: 15px;

  font-family: "Lobster", cursive;
  font-size: 28px;
  font-weight: bold;

  color: #fff;
}

button {
  width: 20%;
  height: 2rem;

  outline: none;

  border: none;
  border-radius: 8px;

  font-size: 16px;

  background: #006ec9;
  color: #fff;

  transition: 300ms;
}

button:hover {
  cursor: pointer;
  background: #19db12;
  width: 21%;

  transition: 100ms;
}

button:focus {
  border: 2px solid #ecd825;
}

.pokemons {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;

  gap: 1.5rem;

  padding: 2rem;

  height: 692px;

  overflow-y: auto;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
  scroll-behavior: smooth;

  margin: 20px;

  box-sizing: border-box;
  box-shadow: 0 0 1em #0004;

  background-attachment: fixed;
}

::-webkit-scrollbar {
  display: none;
}

::-webkit-scrollbar-track {
  background-color: #f4f4f4;
  border-radius: 15px;
}

::-webkit-scrollbar-thumb {
  background: #dad7d7;
  border-radius: 15px;
}
</style>>