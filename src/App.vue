<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokeapi.png" alt="pokeapi" />
      <hr />
      <h4 class="is-size-4">Pokedex</h4>
      <input
        class="input is-primary"
        type="text"
        placeholder="Buscar pokemons pelo nome"
        v-model="busca"
      />
      <!-- <button class="button is-fullwidth is-primary mt-3">Buscar</button> -->
      <div v-for="(poke, index) in resultadoBusca" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";
export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      busca: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((response) => {
        this.pokemons = response.data.results;
      });
  },
  components: { Pokemon },
  computed: {
    resultadoBusca: function () {
      if (this.busca == "" || this.busca == " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter(
          (pokemon) => pokemon.name == this.busca.toLowerCase()
        );
      }
    },
  },
};
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
