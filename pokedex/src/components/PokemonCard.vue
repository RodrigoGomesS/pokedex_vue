<template>
    <div class="gradient">
      <div>
        <v-card-title class="custom-title" align="center">{{ pokemon.name }}</v-card-title>
      </div>
      <div class="image-card">
        <v-img
          :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/${getId(pokemon)}.gif`"
          contain class="responsive-image"></v-img>
      </div>
    </div>
  </template>
  
  <script>
  
  export default {
    name: 'PokemonCard',
    props: {
      pokemon: Object
    },
    methods: {
      getId(pokemon) {
        return pokemon.url.split("/")[6]
      },
    },
  }
  </script>
  
  <style scoped>
  .gradient {
    display: flex;
    justify-content: space-between;
    background: linear-gradient(to bottom, #4b6cb7, #182848);
    border: solid 3px #fff;
    border-radius: 5px;
    min-height: 105px;
    height: 100%;
    margin: 0 auto;
  }

  .image-card{
    min-width: 126px;
    max-height: 105px;
    display: flex;
  align-items: center;
  }
  
  .responsive-image {
    max-width: 50%;
    max-height: auto;
    margin: 0 auto;
  }
  
  .custom-title {
    text-transform: capitalize;
    color: #fff !important;
    font-size: 1rem !important;
  }

  .card-section {
  height: 120px;
}
  </style>
  