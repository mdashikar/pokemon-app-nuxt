<template>
  <div>
    <pokemon-detail
      v-if="pokemonDetails"
      :pokemon-details="pokemonDetails"
      @fetch-next-pokemon="fetchPokemonDetail"
    />
    <not-found v-if="showNotFound" :text="text" />
  </div>
</template>

<script>
import PokemonDetail from '@/components/pokemon/PokemonDetail'
import NotFound from '@/components/pokemon/NotFound'
export default {
  name: 'PokemonRoot',
  components: {
    PokemonDetail,
    NotFound,
  },
  data() {
    return {
      apiBaseUrl: 'https://pokeapi.co/api/v2/pokemon/',
      pokemonDetails: null,
      showNotFound: false,
      text: 'No pokemon details found',
    }
  },
  computed: {
    pokemonId() {
      return this.$route.params.id
    },
  },
  created() {
    this.fetchPokemonDetail(this.pokemonId)
    this.$nuxt.$loading.start()
  },
  methods: {
    fetchPokemonDetail(id) {
      fetch(`${this.apiBaseUrl}${id}`)
        .then((res) => res.json())
        .then((data) => {
          this.pokemonDetails = data
          this.showNotFound = false
          this.$nuxt.$loading.finish()
        })
        .catch((error) => {
          console.log(error)
          this.showNotFound = true
          this.$nuxt.$loading.finish()
        })
    },
  },
}
</script>

<style></style>
