<template>
    <div :class="['d-flex', 'justify-center']">
        <div :class="['background-modal']">
            <div :class="['d-flex', 'align-end', 'container-image']">
                <div :class="['image-modal', 'image-card', `${pokemonType}`]"></div>
                <v-img
                    :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/${pokemonNumero}.gif`"
                    contain :class="['responsive-image']"></v-img>
            </div>
            <div :class="['ml-4']">
                <p :class="['pokeName']">{{ pokemonName }}</p>
                <div :class="['pokeNumero']">N°{{ pokemonNumero }}</div>
                <poke-tag :types="typeList"></poke-tag>
            </div>
        </div>
    </div>
</template>

<script>
import PokeTag from '@/components/PokeTag.vue';

export default {
    name: 'PokemonDialog',

    components:{
        PokeTag,
    },
    props: {
        pokemonName: String,
        pokemonNumero: String,
        pokemonType: String,
        typeList: Array,
    },
}
</script>

<style>
.container-image {
    position: relative;
    min-height: 310px;
}

.background-modal {
    background-color: #fff;
    width: 100%;
    max-width: 360px;
}

.image-modal {
    position: absolute;
    top: 0;
    min-height: 85%;
    width: 100%;
    background-size: 50%;
    border-radius: 0px !important;
    border-bottom-left-radius: 50% !important;
    border-bottom-right-radius: 50% !important;
}

.pokeName {
    font-weight: 500;
    font-size: 32px;
    line-height: 48px;
    color: #000000;
    text-transform: capitalize;
    margin-bottom: 0px !important;
}

.pokeNumero {
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;

    color: rgba(0, 0, 0, 0.7);
}
</style>