<template>
    <div class="d-flex">
        <div :class="[translateType(type.type.name), 'tipo', 'mr-1', 'd-flex', 'align-center']"
            v-for="(type, index) in types" :key="index">
            <div :class="['tag-element', 'd-flex', 'align-center', 'mr-1']">
                <img :class="['responsive-image']" :src="getNameType(translateType(type.type.name))" alt="imagem elemento">
            </div>
            {{ translateType(type.type.name) }}
        </div>
    </div>
</template>

<script>
import água from '../assets/elements/água.png';
import dragão from '../assets/elements/dragão.png';
import elétrico from '../assets/elements/elétrico.png';
import fada from '../assets/elements/fada.png';
import fantasma from '../assets/elements/fantasma.png';
import fogo from '../assets/elements/fogo.png';
import gelo from '../assets/elements/gelo.png';
import grama from '../assets/elements/grama.png';
import inseto from '../assets/elements/inseto.png';
import lutador from '../assets/elements/lutador.png';
import metálico from '../assets/elements/metálico.png';
import normal from '../assets/elements/normal.png';
import pedra from '../assets/elements/pedra.png';
import psíquico from '../assets/elements/psíquico.png';
import sombrio from '../assets/elements/sombrio.png';
import terra from '../assets/elements/terra.png';
import venenoso from '../assets/elements/venenoso.png';
import voador from '../assets/elements/água.png';

export default {
    name: 'PokeTag',
    props: {
        types: Array
    },

    methods: {
        getNameType(typeName) {
            const typeImage = {
                "água": água,
                "dragão": dragão,
                "elétrico": elétrico,
                "fada": fada,
                "fantasma": fantasma,
                "fogo": fogo,
                "gelo": gelo,
                "grama": grama,
                "inseto": inseto,
                "lutador": lutador,
                "metálico": metálico,
                "normal": normal,
                "pedra": pedra,
                "psíquico": psíquico,
                "sombrio": sombrio,
                "terra": terra,
                "venenoso": venenoso,
                "voador": voador,
            };
            return typeImage[typeName];
        },

        translateType(type) {
            // Define um objeto com as traduções de cada tipo
            const translations = {
                "fire": "fogo",
                "water": "água",
                "grass": "grama",
                "bug": "inseto",
                "normal": "normal",
                "poison": "venenoso",
                "electric": "elétrico",
                "ground": "terra",
                "fighting": "lutador",
                "psychic": "psíquico",
                "rock": "pedra",
                "flying": "voador",
                "ghost": "fantasma",
                "ice": "gelo",
                "dragon": "dragão",
                "steel": "metálico",
                "dark": "sombrio",
                "fairy": "fada",
                // Adicione as traduções para os outros tipos
            };
            return translations[type] || type; // Retorna a tradução, ou o próprio nome do tipo caso não tenha tradução
        }

    },
}
</script>

<style>
.tag-element {
    width: 20.31px;
    height: 20.31px;
    background: #FFFFFF;
    border-radius: 50%;
}


.tipo {
    border-radius: 48.6079px;
    padding: 2.90196px 6px;
    text-transform: capitalize;
    font-weight: 500;
    font-size: 11px;
}
</style>