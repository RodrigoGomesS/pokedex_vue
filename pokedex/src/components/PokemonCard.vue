<template>
    <v-card class="gradient">
      <v-img
        :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/${getId(pokemon)}.gif`"
        contain class="responsive-image"></v-img>
      <v-card-title class="d-flex justify-center custom-title" align="center">{{ pokemon.name }}</v-card-title>
      <v-card-subtitle v-for="(type, index) in getType(pokemon)" :key="index">{{ type.type.name }}</v-card-subtitle>
      <v-card-text>{{ pokemon.description }}</v-card-text>
    </v-card>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'PokemonCard',
    props: {
      pokemon: Object
    },
    methods: {
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
  }
  </script>
  
  <style scoped>
  .gradient {
    background: linear-gradient(to bottom, #4b6cb7, #182848);
    border: solid 3px #fff;
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
  