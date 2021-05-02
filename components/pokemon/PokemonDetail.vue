<template>
  <div class="py-8">
    <div class="mx-auto p-2 lg:w-1/3 md:w-1/2 w-full">
      <div
        class="h-full flex items-center border-gray-200 border p-4 rounded-lg"
      >
        <div class="mx-auto">
          <div class="flex flex-col items-center text-center justify-center">
            <div
              class="w-32 h-32 rounded-full inline-flex items-center justify-center bg-gray-200 text-gray-400 mx-auto"
            >
              <img
                alt="team"
                class="w-24 h-24 bg-gray-100 object-cover object-center flex-shrink-0 rounded-full"
                :src="pokemonDetailsData.sprites.front_default"
              />
            </div>
            <h2
              class="font-medium title-font mt-4 text-gray-900 text-lg capitalize"
            >
              {{ pokemonDetailsData.name }}
            </h2>
            <div class="w-12 h-1 bg-indigo-500 rounded mt-2 mb-4"></div>
            <div class="flex space-x-4">
              <button
                v-for="(type, index) in pokemonDetailsData.types"
                :key="index"
                type="button"
                :class="`bg-blue-500 hover:bg-blue-600`"
                class="px-4 py-2 text-xs font-semibold tracking-wider text-white rounded capitalize"
              >
                {{ type.type.name }}
              </button>
            </div>
          </div>
        </div>
      </div>
      <div class="mx-auto sm:max-w-xl md:max-w-full lg:max-w-screen-xl lg:py-8">
        <div class="grid gap-24 row-gap-8 lg:grid-cols-5">
          <div class="grid gap-8 lg:col-span-2">
            <div>
              <p class="mb-2 text-lg font-bold">Species</p>
              <p class="text-gray-700 capitalize">
                {{ pokemonDetailsData.species.name }}
              </p>
            </div>
            <div>
              <p class="mb-2 text-lg font-bold">Moves</p>
              <p class="text-gray-700">
                {{ pokemonDetailsData.moves.length }}
              </p>
            </div>
          </div>
          <div
            class="grid border divide-y rounded lg:col-span-3 sm:grid-cols-2 sm:divide-y-0 sm:divide-x"
          >
            <div class="flex flex-col justify-between p-10">
              <div>
                <p class="text-lg font-semibold text-gray-800 sm:text-base">
                  Height
                </p>
                <p
                  class="text-2xl font-bold text-deep-purple-accent-400 sm:text-xl"
                >
                  {{ pokemonDetailsData.height }}
                </p>
              </div>
            </div>
            <div class="flex flex-col justify-between p-10">
              <div>
                <p class="text-lg font-semibold text-gray-800 sm:text-base">
                  Weight
                </p>
                <p
                  class="text-2xl font-bold text-deep-purple-accent-400 sm:text-xl"
                >
                  {{ pokemonDetailsData.weight }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="overflow-x-auto mt-6">
        <table class="table-auto border-collapse w-full">
          <thead class="bg-gray-200">
            <tr class="rounded-lg font-medium text-gray-700 text-left text-md">
              <th class="px-4 py-2"></th>
              <th class="px-4 py-2">Base stats</th>
              <th class="px-4 py-2">Efforts</th>
            </tr>
          </thead>
          <tbody class="text-sm font-normal text-gray-700">
            <tr
              v-for="(stat, index) in pokemonDetailsData.stats"
              :key="index"
              class="hover:bg-gray-100 border-b border-gray-200 py-10"
            >
              <td class="px-4 py-4 capitalize">{{ stat.stat.name }}</td>
              <td class="px-4 py-4">{{ stat.base_stat }}</td>
              <td class="px-4 py-4">{{ stat.effort }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'PokemonDetail',
  props: {
    pokemonDetails: { type: Object, default: null },
  },
  data() {
    return {
      colors: ['red', 'yellow', 'green', 'pink', 'indigo', 'purple'],
    }
  },
  computed: {
    pokemonDetailsData() {
      return this.pokemonDetails
    },
    randomColor() {
      const random = Math.floor(Math.random() * this.colors.length)
      return this.colors[random]
    },
  },
  methods: {
    getTypes(types) {
      return types.map((type) => type.type.name).join(', ')
    },
    randomBgColor() {
      const random = Math.floor(Math.random() * this.colors.length)
      return this.colors[random]
    },
  },
}
</script>
