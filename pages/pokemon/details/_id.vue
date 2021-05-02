<template>
  <div>
    <pokemon-detail
      v-if="pokemonDetails"
      :pokemon-details="pokemonDetails"
      @fetch-next-pokemon="fetchPokemonDetail"
    />
  </div>
</template>

<script>
import PokemonDetail from '@/components/pokemon/PokemonDetail'
export default {
  name: 'PokemonRoot',
  components: {
    PokemonDetail,
  },
  data() {
    return {
      apiBaseUrl: 'https://pokeapi.co/api/v2/pokemon/',
      pokemonDetails: null,
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
          this.$nuxt.$loading.finish()
        })
        .catch((error) => {
          console.log(error)
          this.$nuxt.$loading.finish()
        })
    },
  },
}
</script>

<style></style>
