<template>
    <div :class="['gradient', typeClass]">
      <div>
        <v-card-title class="custom-title" align="center">{{ pokemon.name }}</v-card-title>
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
    };
  },

    methods: {
      getId(pokemon) {
        return pokemon.url.split("/")[6]
      },

      async getPokemon(id){
  const response = await axios.get(`https://pokeapi.co/api/v2/pokemon/${id}`);
  const pokemon = response.data;
  return pokemon;
},

async getFirstType(id) {
  const result = await this.getPokemon(id);
  const primaryType = result.types[0].type.name;
  this.typeClass = primaryType; 
  console.log(this.typeClass)
}

    },

    created() {
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

  .image-card{
    border-radius: 10px;
    min-width: 126px;
    max-height: 105px;
    display: flex;
  align-items: center;
  /*background-image: url('../assets/dark.png');*/
  }
  
  .responsive-image {
    max-width: 50%;
    max-height: auto;
    margin: 0 auto;
  }
  
  .custom-title {
    text-transform: capitalize;
    color: #000000 !important;
    font-size: 1rem !important;
  }

  .card-section {
  height: 120px;
}

.image-card.grass { background-color: #63BC5A;
  background-image: url('../assets/grass.png');
  background-position: center;
}
.image-card.fire { background-color: #FF9D55; 
  background-image: url('../assets/fire.png');
  background-position: center;
}
.image-card.water { background-color: #5090D6;
  background-image: url('../assets/water.png');
  background-position: center;
 }
.image-card.bug { background-color: #91C12F;
   background-image: url('../assets/bug.png');
  background-position: center;
 }
.image-card.normal { background-color: #919AA2;
  background-image: url('../assets/normal.png');
  background-position: center;
}
.image-card.poison { background-color: #B567CE;
  background-image: url('../assets/poison.png');
  background-position: center;
}
.image-card.electric { background-color: #F4D23C;
  background-image: url('../assets/electric.png');
  background-position: center;
}
.image-card.ground { background-color: #D97845;
  background-image: url('../assets/ground.png');
  background-position: center;
}
.image-card.fighting { background-color: #CE416B;
  background-image: url('../assets/fighting.png');
  background-position: center;
}
.image-card.psychic { background-color: #FA7179;
  background-image: url('../assets/psychic.png');
  background-position: center;
}
.image-card.rock { background-color: #C5B78C;
  background-image: url('../assets/rock.png');
  background-position: center;
}
.image-card.flying { background-color: #89AAE3;
  background-image: url('../assets/flying.png');
  background-position: center;
}
.image-card.ghost { background-color: #5269AD;
  background-image: url('../assets/ghost.png');
  background-position: center;
}
.image-card.ice { background-color: #73CEC0;
  background-image: url('../assets/ice.png');
  background-position: center;
}
.image-card.dragon { background-color: #0B6DC3; 
  background-image: url('../assets/dragon.png');
  background-position: center;
}
.image-card.steel { background-color: #5A8EA2; 
  background-image: url('../assets/steel.png');
  background-position: center;
} 
.image-card.dark { background-color: #5A5465;
  background-image: url('../assets/dark.png');
  background-position: center;
} 
.image-card.fairy { background-color: #EC8FE6;
  background-image: url('../assets/fairy.png');
  background-position: center;
}
.grass.gradient { background-color: #EDF6EC; }
.fire.gradient { background-color: #FCF3EB; }
.water.gradient { background-color: #EBF1F8; }
.bug.gradient { background-color: #F1F6E8; }
.normal.gradient { background-color: #F1F2F3; }
.poison.gradient { background-color: #F5EDF8; }
.electric.gradient { background-color: #FBF8E9; }
.ground.gradient { background-color: #F9EFEA; }
.fighting.gradient { background-color: #F8E9EE; }
.psychic.gradient { background-color: #FCEEEF; }
.rock.gradient { background-color: #F7F5F1; }
.flying.gradient { background-color: #F1F4FA; }
.ghost.gradient { background-color: #EBEDF4; }
.ice.gradient { background-color: #F1FBF9; }
.dragon.gradient { background-color: #E4EEF6; }
.steel.gradient { background-color: #ECF1F3; } 
.dark.gradient { background-color: #ECEBED; } 
.fairy.gradient { background-color: #FBF1FA; }

  </style>
  