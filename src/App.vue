<template>
  <div id="app">
    <div v-for="(poke, index) in pokemons" :key="index">
      <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from './components/Pokemon.vue';
export default {
  name: "App",
  data() {
    return {
      pokemons: [],
    };
  },
  created: function () {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((response) => {
        console.log("Carregou pokemons");
        this.pokemons = response.data.results;
        console.log(this.pokemons);
      });
  },
  components: { Pokemon }
};
</script>

<style>
</style>
