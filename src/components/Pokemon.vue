<template>
  <div class="pokemon">
    <img :src="currentImage" @click="changeImage" alt="" />
    <div class="stats">
      <h1>{{ pokemon.name | firstLetterToUpperCase }}</h1>
      <strong
        >Type: {{ pokemon.types[0].type.name | firstLetterToUpperCase }}</strong
      >
      <div class="physical-status">
        <strong>Height: {{ pokemon.height }}</strong>
        <strong>Weight: {{ pokemon.weight }}</strong>
      </div>
      <span v-for="(status, index) in pokemon.stats" :key="index">
        {{ status.stat.name }} {{ status.base_stat }}
      </span>
    </div>
  </div>
</template>

<script>
import api from "../services/api";

export default {
  name: "Pokemon",
  props: {
    number: Number,
    name: String,
  },
  created: function () {
    api.get(`pokemon/${this.number}`).then((response) => {
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
.pokemon {
  display: flex;
  flex-direction: column;
  align-items: center;

  background: #f1f1f1;

  box-shadow: 0 0 1em #0004;

  margin: 1.4rem;
}

.stats {
  background: #d3d3d3;

  padding: 0 12px 30px 12px;

  width: 100%;
  height: 50%;

  border-radius: 6px;
  box-shadow:1 1 1 1em #0004;
}

img {
  width: 100%;
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
  width: 105%;
}
</style>