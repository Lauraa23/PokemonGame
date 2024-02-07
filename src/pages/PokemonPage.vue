<template>
  <h1 v-if="!pokemon">Espere por favor...</h1>
  <div v-else class="container">
    <h1>¿Cuál es este pokémon?</h1>

    <pokemon-picture :pokemonId="pokemon.id" :showPokemon="showPokemon" />

    <pokemon-options :pokemons="pokemonArr" @selection="checkAnswer" />
    <div v-if="showAnswer">
      <h2 class="fade-in">{{ message }}</h2>

      <button @click="newGame">Nuevo Juego</button>
    </div>
  </div>
</template>
<script>
import PokemonPicture from "@/components/PokemonPicture.vue";
import PokemonOptions from "@/components/PokemonOptions.vue";
import getPokemonsOptions from "@/helpers/getPokemonOptions";

//console.log(getPokemonsOptions());

export default {
  components: {
    PokemonOptions,
    PokemonPicture,
  },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
    };
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonsOptions();

      const rndInt = Math.floor(Math.random() * 4);

      this.pokemon = this.pokemonArr[rndInt];
    },
    checkAnswer(selectedId) {
      this.showPokemon = true;
      this.showAnswer = true;

      if (selectedId === this.pokemon.id) {
        this.message = `Correcto, ${this.pokemon.name}`;
      } else {
        this.message = `Oops, era ${this.pokemon.name}`;
      }
    },
    newGame() {
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemonArr = [];
      this.pokemon = null;
      this.mixPokemonArray();
    },
  },
  mounted() {
    this.mixPokemonArray();
  },
};
</script>
<style>
.container{
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
button {
  border: 1px solid #00000033;
  border-radius: 50px;
  cursor: pointer;
  background-color: white;
  text-align: center;
  
}
button:hover {
  background-color: #00ffaa0d;
}
</style>
