<template>
    <div class="pokemon-container">
        <img class="hidden-pokemon" :src="imgSrc" alt="pokemon">
        <img v-if="showPokemon" class="fade-in" :src="imgSrc" alt="pokemon">
    </div>
</template>

<script>
export default {
    props: {
        pokemonId: {
            type: Number,
            required: true
        },
        showPokemon: {
            type: Boolean,
            required: true,
            default: false
        }
    },
    // name:"PokemonPicture"
    computed: {
        imgSrc(){
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`
        }
    }
}
</script>

<style scoped>

.pokemon-container {
    position: relative;
    height: 18rem;
}
img {
    height: 200px;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
    user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -webkit-user-drag: none;
    -webkit-user-select: none;
}

.hidden-pokemon {
    filter: brightness(0)
}

</style>