<template>
  <div :class="['gradient', typeClass]">
    <div class="ml-4 d-flex flex-column justify-center">
      <div class="pokeNumero">N°{{ getId(pokemon) }}</div>
      <div class="custom-title">{{ pokemon.name }}</div>
      <div class="d-flex">
        <div :class="[translateType(type.type.name), 'tipo', 'mr-1', 'd-flex','align-center']" v-for="(type, index) in types" :key="index">
          <div :class="['tag-element','d-flex','align-center','mr-1']">
            <img :class="['responsive-image']" src="../assets/elements/normal.png" alt="imagem elemento">
          </div>
        {{translateType(type.type.name) }}
      </div>
      </div>
    </div>
    <div :class="['image-card', typeClass]">
      <v-img
        :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/${getId(pokemon)}.gif`"
        contain class="responsive-image"></v-img>
    </div>
  </div>
</template>
  
<script>
import axios from 'axios';

export default {
  name: 'PokemonCard',
  props: {
    pokemon: Object
  },

  data() {
    return {
      typeClass: '', // inicializa typeClass como uma string vazia
      types: [], // Inicializa a variável types como um array vazio
    };
  },

  methods: {
    getId(pokemon) {
      return pokemon.url.split("/")[6]
    },

    async getPokemon(id) {
      const response = await axios.get(`https://pokeapi.co/api/v2/pokemon/${id}`);
      const pokemon = response.data;
      return pokemon;
    },

    async getFirstType(id) {
      const result = await this.getPokemon(id);
      const primaryType = result.types[0].type.name;
      this.typeClass = primaryType;
    },

    async getTypes(id) {
      const result = await this.getPokemon(id);
      const types = result.types;
      this.types = types; // Define a variável types com o array de tipos
    },

    translateType(type) {
      // Define um objeto com as traduções de cada tipo
      const translations = {
        'fire': 'fogo',
        'water': 'água',
        'grass': 'grama',
        'bug': 'inseto',
        'normal': 'normal',
        'poison': 'venenoso',
        'electric': 'elétrico',
        'ground': 'terra',
        'fighting': 'lutador',
        'psychic': 'psíquico',
        'rock': 'pedra',
        'flying': 'voador',
        'ghost': 'fantasma',
        'ice': 'gelo',
        'dragon': 'dragão',
        'steel': 'metálico',
        'dark': 'sombrio',
        'fairy': 'fada',


        // Adicione as traduções para os outros tipos
      };
      return translations[type] || type; // Retorna a tradução, ou o próprio nome do tipo caso não tenha tradução
    }
  },

  created() {
    this.getTypes(this.getId(this.pokemon));
    this.getFirstType(this.getId(this.pokemon));
  },
}
</script>

<style scoped>
.gradient {
  display: flex;
  justify-content: space-between;
  border-radius: 10px;
  min-height: 105px;
  height: 100%;
  margin: 0 auto;
}

.image-card {
  border-radius: 10px;
  min-width: 126px;
  max-height: 105px;
  display: flex;
  align-items: center;
  /*background-image: url('../assets/dark.png');*/
}

.tag-element{
 width: 20.31px;
height: 20.31px;
background: #FFFFFF;
border-radius: 50%;
}

.responsive-image {
  max-width: 50%;
  max-height: auto;
  margin: 0 auto;
}

.custom-title {
  text-transform: capitalize;
  color: #000000 !important;
  font-weight: 600;
  font-size: 21px;
}

.card-section {
  height: 120px;
}

.pokeNumero {
  font-weight: 600;
  font-size: 12px;
  color: #333333;
}

.tipo {
  border-radius: 48.6079px;
  padding: 2.90196px 6px;
  text-transform: capitalize;
  font-weight: 500;
  font-size: 11px;
}

.image-card.grass,
.grama {
  background-color: #63BC5A;
  background-image: url('../assets/background-element/grass.png');
  background-position: center;
}

.grama {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.fire,
.fogo {
  background-color: #FF9D55;
  background-image: url('../assets/background-element/fire.png');
  background-position: center;
}

.fogo {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.water,
.água {
  background-color: #5090D6;
  background-image: url('../assets/background-element/water.png');
  background-position: center;
}

.água {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.bug,
.inseto {
  background-color: #91C12F;
  background-image: url('../assets/background-element/bug.png');
  background-position: center;
}

.inseto {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.normal,
.normal {
  background-color: #919AA2;
  background-image: url('../assets/background-element/normal.png');
  background-position: center;
}

.normal {
  background-image: unset;
  background-position: unset;
}

.image-card.poison,
.venenoso {
  background-color: #B567CE;
  background-image: url('../assets/background-element/poison.png');
  background-position: center;
}

.venenoso {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.electric,
.elétrico {
  background-color: #F4D23C;
  background-image: url('../assets/background-element/electric.png');
  background-position: center;
}

.elétrico {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.ground,
.terra {
  background-color: #D97845;
  background-image: url('../assets/background-element/ground.png');
  background-position: center;
}

.terra {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.fighting,
.lutador {
  background-color: #CE416B;
  background-image: url('../assets/background-element/fighting.png');
  background-position: center;
}

.lutador {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.psychic,
.psíquico {
  background-color: #FA7179;
  background-image: url('../assets/background-element/psychic.png');
  background-position: center;
}

.psíquico {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.rock,
.pedra {
  background-color: #C5B78C;
  background-image: url('../assets/background-element/rock.png');
  background-position: center;
}

.pedra {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.flying,
.voador {
  background-color: #89AAE3;
  background-image: url('../assets/background-element/flying.png');
  background-position: center;
}

.voador {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.ghost,
.fantasma {
  background-color: #5269AD;
  background-image: url('../assets/background-element/ghost.png');
  background-position: center;
}

.fantasma {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.ice,
.gelo {
  background-color: #73CEC0;
  background-image: url('../assets/background-element/ice.png');
  background-position: center;
}

.gelo {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.dragon,
.dragão {
  background-color: #0B6DC3;
  background-image: url('../assets/background-element/dragon.png');
  background-position: center;
}

.dragão {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.steel,
.metálico {
  background-color: #5A8EA2;
  background-image: url('../assets/background-element/steel.png');
  background-position: center;
}

.metálico {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.dark,
.sombrio {
  background-color: #5A5465;
  background-image: url('../assets/background-element/dark.png');
  background-position: center;
}

.sombrio {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;
}

.image-card.fairy,
.fada {
  background-color: #EC8FE6;
  background-image: url('../assets/background-element/fairy.png');
  background-position: center;
}

.fada {
  background-image: unset;
  background-position: unset;
  border-radius: 48px;  
}

.grass.gradient {
  background-color: #EDF6EC;
}

.fire.gradient {
  background-color: #FCF3EB;
}

.water.gradient {
  background-color: #EBF1F8;
}

.bug.gradient {
  background-color: #F1F6E8;
}

.normal.gradient {
  background-color: #F1F2F3;
}

.poison.gradient {
  background-color: #F5EDF8;
}

.electric.gradient {
  background-color: #FBF8E9;
}

.ground.gradient {
  background-color: #F9EFEA;
}

.fighting.gradient {
  background-color: #F8E9EE;
}

.psychic.gradient {
  background-color: #FCEEEF;
}

.rock.gradient {
  background-color: #F7F5F1;
}

.flying.gradient {
  background-color: #F1F4FA;
}

.ghost.gradient {
  background-color: #EBEDF4;
}

.ice.gradient {
  background-color: #F1FBF9;
}

.dragon.gradient {
  background-color: #E4EEF6;
}

.steel.gradient {
  background-color: #ECF1F3;
}

.dark.gradient {
  background-color: #ECEBED;
}

.fairy.gradient {
  background-color: #FBF1FA;
}
</style>
  