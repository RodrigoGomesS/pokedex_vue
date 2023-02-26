<template>
  <v-app>
    <pokedex-menu :filter-value="filterValue" @filter-pokemons="filterPokemons" />
    <v-container>
      <v-row>
        <v-col cols="12" sm="3" v-for="pokemon in paginatedPokemons" :key="pokemon.name">
          <pokemon-card :pokemon="pokemon" />
        </v-col>
      </v-row>
    </v-container>
    <v-pagination
  v-model="page"
  :length="Math.ceil(filteredPokemons.length / itemsPerPage)"
  :total-visible="5"
  circle
/>
  </v-app>
</template>

<script>

import axios from 'axios';
import PokedexMenu from '@/components/Menu.vue';
import PokemonCard from '@/components/PokemonCard.vue';

export default {
  name: 'App',

  components: {
    PokedexMenu,
    PokemonCard,
  },

  data() {
    return {
      pokemons: [],
      filterValue: "",
      page: 1,
    itemsPerPage: 10
    }
  },

  computed: {
    filteredPokemons() {
      if (this.filterValue) {
        return this.pokemons.filter((pokemon) =>
          pokemon.name.toLowerCase().includes(this.filterValue)
        );
      } else {
        return this.pokemons;
      }
    },

    paginatedPokemons() {
    const startIndex = (this.page - 1) * this.itemsPerPage;
    return this.filteredPokemons.slice(startIndex, startIndex + this.itemsPerPage);
  }
  },

  mounted() {
    axios.get(" https://pokeapi.co/api/v2/pokemon?limit=1000").then((response) => {
      this.pokemons = response.data.results
    })

  },

  methods: {
    filterPokemons(value) {
      this.filterValue = value;
      this.page = 1;
    },
  },

};
</script>

<style>
#app {
  background: linear-gradient(to bottom, #a40808, #e73939) no-repeat center center fixed !important;
  background-size: cover !important;
  background-position: center;
  min-height: 100vh;
}

</style>
