<template>
  <div class="container px-5 py-5 mx-auto">
    <search @searched-text="fetchPokemon" />
    <pokemon-card v-if="showSearchResult" :pokemon-info="pokemonInfo" />
  </div>
</template>
<script>
import Search from './PokemonSearch'
export default {
  name: 'PokemonRoot',
  components: {
    Search,
  },
  data() {
    return {
      apiBaseUrl: 'https://pokeapi.co/api/v2/pokemon/',
      pokemonInfo: null,
      showSearchResult: false,
    }
  },
  methods: {
    fetchPokemon(pokemonName) {
      fetch(`${this.apiBaseUrl}${pokemonName}`)
        .then((res) => res.json())
        .then((data) => {
          this.showSearchResult = true
          this.pokemonInfo = data
        })
        .catch((error) => {
          console.log(error)
          this.showSearchResult = false
        })
    },
  },
}
</script>
