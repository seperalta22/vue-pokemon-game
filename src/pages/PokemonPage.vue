<template>
  <h1 v-if="!pokemon">Espere por favor...</h1>
  <div v-else>
    <h1>¿Quién es este Pokémon?</h1>
    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon"/>
    <PokemonOptions :pokemons="pokemonArray" @selection="checkAnswer($event)"/>
    <div v-if="showAnswer">
      <h2 class="fade-in">{{ message }}</h2>
      <button @click="newGame"> Nuevo Juego</button>
    </div>
  </div>
</template>
<script>
import PokemonPicture from '../components/PokemonPicture.vue';
import PokemonOptions from '../components/PokemonOptions.vue';
import getPokeOptions from '@/helpers/getPokeOptions';

getPokeOptions();


export default {
  components: {
    PokemonPicture,
    PokemonOptions,
  },
  data() {
    return {
      pokemonArray: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: '',
    };
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArray = await getPokeOptions();

      const rndInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokemonArray[rndInt];
    },
    checkAnswer(selectedId) {
      this.showPokemon = true;
      this.showAnswer = true;

      if (selectedId === this.pokemon.id) {
        this.message = '¡Correcto!';
      } else {
        this.message = `Ooops, era ${this.pokemon.name.charAt(0).toUpperCase() + this.pokemon.name.slice(1)}!`;
      }
    },
    newGame() {
      this.pokemon = null;
      this.pokemonArray = [];
      this.showPokemon = false;
      this.showAnswer = false;
      this.mixPokemonArray();
    },
  },
  mounted() {
    return this.mixPokemonArray();
  },
};
</script>
