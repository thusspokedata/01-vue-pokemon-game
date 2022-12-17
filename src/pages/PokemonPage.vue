<template>
  <h1 v-if="!pokemon">Espere por favor...</h1>
  <div v-else>
    <h1>Quien es este pokemon?</h1>
    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
    <PokemonOptions 
      :pokemons="pokemonArr"
      @selection="checkAnswer"
    />
    <template v-if="showAnswer">
      <h2 class="fade-in">{{message}}</h2>
      <button @click="newGame">Nuevo juego</button>
    </template>
  </div>
</template>

<script>

import PokemonPicture from '@/components/PokemonPicture.vue'
import PokemonOptions from '@/components/PokemonOptions.vue'

import getPokemonOptions from '@/helpers/getPokemonOptions'

console.log(getPokemonOptions())

export default {
  name: 'PokemonPage',
  components: {
    PokemonPicture,
    PokemonOptions,
  }, 
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: ''
    }
  },
  methods: {
    async mixPokemonArr() {
      this.pokemonArr = await getPokemonOptions()
      console.log(this.pokemonArr)

      const rndInt = Math.floor(Math.random() * 4)
      this.pokemon = this.pokemonArr[ rndInt ]
    },
    checkAnswer(pokemonId){
      
      if (pokemonId === this.pokemon.id) {
        this.showPokemon = true
        this.showAnswer= true
        this.message = `Correcto, el nombre del pokemon es ${this.pokemon.name.toUpperCase()}!`
      } else {
        this.showAnswer= true
        this.message = `Ops, este no es el nombre del pokemon!`
      }
    },
    newGame(){
      this.pokemonArr= [],
      this.pokemon= null,
      this.showPokemon= false,
      this.showAnswer= false,
      this.mixPokemonArr()
    }
  }, 
  mounted() {
    this.mixPokemonArr()
  }
}
</script>
