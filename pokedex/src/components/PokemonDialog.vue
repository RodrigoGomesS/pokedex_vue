<template>
    <div :class="['d-flex', 'justify-center']">
        <div :class="['background-modal']">
            <div :class="['image-modal','d-flex', 'align-end','image-card', `${pokemonType}`]">
                <v-img
        :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/${pokemonNumero}.gif`"
        contain :class="['responsive-image']"></v-img>
            </div>
            <div :class="['ml-4']">
                <p :class="['pokeName']">{{ pokemonName }}</p>
               <div :class="['pokeNumero']">N°{{ pokemonNumero }}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'PokemonDialog',
  props: {
    pokemonName: String,
    pokemonNumero: String,
    pokemonType: String
  },
}
</script>

<style>
.background-modal{
    background-color: #fff;
    width: 100%;
    max-width: 360px;
}

.image-modal{
    min-height: 310px;
    border-radius: 0px !important;
    border-bottom-left-radius: 50% !important;
    border-bottom-right-radius: 50% !important;
}

.pokeName{
font-weight: 500;
font-size: 32px;
line-height: 48px;
color: #000000;
text-transform: capitalize;
margin-bottom: 0px !important;
}

</style>