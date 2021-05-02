<template>
  <div>
    <pokemon-detail v-if="pokemonDetails" :pokemon-details="pokemonDetails" />
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
    this.fetchPokemonDetail()
  },
  methods: {
    fetchPokemonDetail() {
      fetch(`${this.apiBaseUrl}${this.pokemonId}`)
        .then((res) => res.json())
        .then((data) => {
          this.pokemonDetails = data
        })
        .catch((error) => {
          console.log(error)
        })
    },
  },
}
</script>

<style></style>
