<template>
  <div class="pokemon-container">
    <img class="pokemon-hidden" :src="imgSrc" alt="pokemon" />
    <img v-if="showPokemon" class="fade-in" :src="imgSrc" alt="pokemon" />
  </div>
</template>
<script>
export default {
  props: {
    pokemonId: {
      type: Number,
      required: true,
    },
    showPokemon: {
      type: Boolean,
      required: true,
      default: false,
    },
  },
  computed: {
    imgSrc() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`;
    },
  },
};
</script>
<style scoped>
.pokemon-container {
  height: 200px;
  
}
img {
  height: 200px;
  position: absolute;
  width: 100vw;
  margin-left: -50vw;
  user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
  filter: drop-shadow(0 2px 5px #000000b3);
  
}
.pokemon-hidden {
  filter: brightness(0);
}
</style>
