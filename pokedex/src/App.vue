<template>
  <v-app>
    <pokedex-menu :filter-value="filterValue" @filter-pokemons="filterPokemons" />
    <v-container>
      <v-row>
        <v-col cols="12" sm="6" lg="4" v-for="pokemon in paginatedPokemons" :key="pokemon.name">
          <pokemon-card :pokemon="pokemon" />
        </v-col>
      </v-row>
    </v-container>
    <pokedex-error message="Nenhum pokémon encontrado." :show="showError" />
    <poke-pagination :items="filteredPokemons" :filter-value="filterValue" :items-per-page="itemsPerPage"
      :page.sync="page" v-if="!showError" />
  </v-app>
</template>

<script>

import axios from 'axios';
import PokedexMenu from '@/components/Menu.vue';
import PokemonCard from '@/components/PokemonCard.vue';
import PokePagination from '@/components/PokePagination.vue';
import PokedexError from "@/components/PokedexError.vue";

export default {
  name: 'App',

  components: {
    PokedexMenu,
    PokemonCard,
    PokePagination,
    PokedexError,
  },

  data() {
    return {
      pokemons: [],
      filterValue: "",
      page: 1,
      itemsPerPage: 12,
      showError: false,
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
      this.showError = this.filteredPokemons.length === 0 && this.filterValue !== "";
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
