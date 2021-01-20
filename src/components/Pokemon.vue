<template>
  <div class="pokemon">
    <img :src="currentImage" @click="changeImage" alt="" />
    <div class="stats">
      <span>N° {{ pokemon.id }}</span>
      <h1>{{ name | firstLetterToUpperCase }}</h1>
      <strong
        :class="{
          'type-grass': pokemon.types[0].type.name === 'grass',
          'type-fire': pokemon.types[0].type.name === 'fire',
          'type-water': pokemon.types[0].type.name === 'water',
          'type-bug': pokemon.types[0].type.name === 'bug',
          'type-poison': pokemon.types[0].type.name === 'poison',
          'type-normal': pokemon.types[0].type.name === 'normal',
          'type-electric': pokemon.types[0].type.name === 'electric',
          'type-ground': pokemon.types[0].type.name === 'ground',
          'type-fairy': pokemon.types[0].type.name === 'fairy',
          'type-fighting': pokemon.types[0].type.name === 'fighting',
          'type-psychic': pokemon.types[0].type.name === 'psychic',
          'type-rock': pokemon.types[0].type.name === 'rock',
          'type-ghost': pokemon.types[0].type.name === 'ghost',
        }"
        >{{ pokemon.types[0].type.name | firstLetterToUpperCase }}</strong
      >
      <div class="physical-status">
        <strong>Height: {{ pokemon.height }}</strong>
        <strong>Weight: {{ pokemon.weight }}</strong>
      </div>
      <div class="pokestats">
        <span v-for="(status, index) in pokemon.stats" :key="index">
          {{ status.stat.name.toUpperCase() }}: {{ status.base_stat }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Pokemon",
  props: {
    number: Number,
    name: String,
    url: String,
  },
  created: function () {
    axios.get(this.url).then((response) => {
      this.pokemon = response.data;
      this.currentImage = this.pokemon.sprites.front_default;
    });
  },
  data() {
    return {
      isFront: true,
      currentImage: "",
      pokemon: {},
    };
  },
  filters: {
    firstLetterToUpperCase: function (name) {
      return name[0].toUpperCase() + name.slice(1);
    },
  },
  methods: {
    changeImage() {
      if (this.isFront) {
        this.currentImage = this.pokemon.sprites.back_default;
        this.isFront = !this.isFront;
      } else {
        this.currentImage = this.pokemon.sprites.front_default;
        this.isFront = !this.isFront;
      }
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Lobster&display=swap");

.pokemon {
  display: flex;
  flex-direction: column;
  align-items: center;

  background: #0004;

  box-shadow: 0 0 1em #0004;
  box-sizing: border-box;
  margin: 1.4rem;
}

img {
  width: 97%;
  height: 50%;

  image-rendering: -moz-crisp-edges;
  image-rendering: -webkit-crisp-edges;
  image-rendering: pixelated;
  image-rendering: crisp-edges;

  object-fit: cover;

  transition: 300ms;
}

img:hover {
  cursor: pointer;
  width: 100%;
}

.stats {
  display: flex;
  flex-direction: column;
  align-items: center;

  background: #f5f5f5;

  padding: 12px;

  width: 100%;
  height: 50%;

  border-radius: 6px;
  box-shadow: 1 1 1 1em #0004;
}

span {
  align-self: flex-start;
}

h1 {
  font-family: "Lobster", cursive;
}

strong {
  width: 80%;
  height: 1.2rem;

  margin-bottom: 0.8rem;
  border-radius: 6px;
}

strong.type-grass {
  background: rgb(53, 211, 21);
}

strong.type-fire {
  background: rgb(211, 59, 21);
}

strong.type-water {
  background: rgb(21, 173, 211);
}

strong.type-bug {
  background: rgb(122, 80, 0);
  color: #fff;
}

strong.type-poison {
  background: rgb(157, 21, 211);
  color: #fff;
}

strong.type-normal {
  background: rgb(197, 221, 210);
}

strong.type-electric {
  background: rgb(255, 251, 17);
}

strong.type-ground {
  background: rgb(170, 105, 19);
  color: #fff;
}

strong.type-fighting {
  background: rgb(107, 94, 59);
}

strong.type-fairy {
  background: rgb(255, 83, 226);
}

strong.type-Psychic {
  background: rgb(211, 21, 186);
  color: #fff;
}

strong.type-rock {
  background: rgb(59, 59, 59);
  color: #fff;
}

strong.type-ghost {
  background: rgb(255, 255, 255);
}

.physical-status {
  display: flex;
  justify-content: space-between;
  align-items: center;

  width: 100%;
}

.pokestats {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;

  font-size: 12px;
}

</style>