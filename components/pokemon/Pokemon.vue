<template>
  <div class="container px-5 py-5 mx-auto">
    <search
      @searched-text="fetchPokemon"
      @clear-search-data="clearSearchData"
    />
    <pokemon-card v-if="showSearchResult" :pokemon-info="pokemonInfo" />
    <not-found v-if="showNotFound" :text="text" />
  </div>
</template>
<script>
import NotFound from './NotFound.vue'
import Search from './PokemonSearch'
export default {
  name: 'PokemonRoot',
  components: {
    Search,
    NotFound,
  },
  data() {
    return {
      apiBaseUrl: 'https://pokeapi.co/api/v2/pokemon/',
      pokemonInfo: null,
      showSearchResult: false,
      showNotFound: false,
      text: 'No pokemon found',
    }
  },
  methods: {
    clearSearchData() {
      this.showSearchResult = false
      this.showNotFound = false
      this.pokemonInfo = null
    },
    fetchPokemon(pokemonName) {
      this.$nuxt.$loading.start()
      fetch(`${this.apiBaseUrl}${pokemonName}`)
        .then((res) => res.json())
        .then((data) => {
          this.$nuxt.$loading.finish()
          this.showSearchResult = true
          this.showNotFound = false
          this.pokemonInfo = data
        })
        .catch(() => {
          this.$nuxt.$loading.finish()
          this.showNotFound = true
          this.showSearchResult = false
        })
    },
  },
}
</script>
