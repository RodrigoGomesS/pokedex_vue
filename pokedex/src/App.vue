<template>
  <v-app>
    <pokedex-menu :filter-value="filterValue" @filter-pokemons="filterPokemons" />
    <v-container>
      <v-row>
        <v-col cols="12" sm="3" v-for="pokemon in paginatedPokemons" :key="pokemon.name">
          <v-card class="gradient">
            <v-img
              :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/${getId(pokemon)}.gif`"
              contain class="responsive-image"></v-img>
            <v-card-title class="d-flex justify-center custom-title" align="center">{{ pokemon.name }}</v-card-title>
            <v-card-subtitle v-for="(type, index) in getType(pokemon)" :key="index">{{ type.type.name }}</v-card-subtitle>
            <v-card-text>{{ pokemon.description }}</v-card-text>
          </v-card>
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
export default {
  name: 'App',

  components: {
    PokedexMenu,
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

    getId(pokemon) {
      return pokemon.url.split("/")[6]
    },

    async getType(pokemon) {
      try {
        let id = this.getId(pokemon)
        const response = await axios.get(`https://pokeapi.co/api/v2/pokemon/${id}`);
        const result = response.data;

        // Para acessar o tipo do Pokemon, você pode usar a propriedade "types" do objeto retornado.
        // const pokemonTypes = result.types.map(type => type.type.name);
        return result;
      } catch (error) {
        console.error(error);
      }
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

.gradient {
  background: linear-gradient(to bottom, #4b6cb7, #182848);
  border: solid 3px transparent;
  background-clip: padding-box;
  padding-top: 2rem;
}

.gradient:before {
  content: '';
  position: absolute;
  top: -3px;
  left: -3px;
  right: -3px;
  bottom: -3px;
  background: linear-gradient(to bottom, #6e7277, #434649) !important;
  z-index: -1;
}

.responsive-image {
  max-width: 100%;
  max-height: 80px;
}

.custom-title {
  text-transform: capitalize;
  color: #fff !important;
}
</style>
