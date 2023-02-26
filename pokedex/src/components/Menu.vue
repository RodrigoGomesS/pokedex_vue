<template>
    <v-app-bar app color="#ff0000" class="menu-bar">


        <div class="d-flex">
            <v-avatar class="blue-gradient">
            </v-avatar>
            <div class="d-flex">
                <v-avatar class="red-gradient blinking-red">
                </v-avatar>
                <v-avatar class="yellow-gradient blinking-yellow">
                </v-avatar>
                <v-avatar class="green-gradient blinking-green ">
                </v-avatar>
            </div>
        </div>
        <v-responsive class="mx-auto" max-width="200">
            <v-text-field v-model="search" append-icon="mdi-magnify" dark label="Pesquisar" @input="filterPokemons"
                placeholder="Nome do Pokémon" hide-details solo-inverted @keydown.enter="filterPokemons">
            </v-text-field>
        </v-responsive>

    </v-app-bar>
</template>

<script>
export default {
    name: 'PokedexMenu',

    data() {
        return {
            drawer: false,
            search: ''
        }
    },
    methods: {
        searchPokemon() {
            // Implementar a busca aqui, por exemplo:
            console.log(`Buscando por ${this.search}`);
        },
        filterPokemons() {
            this.$emit("filter-pokemons", this.search.toLowerCase());
        },
    },
}
</script>

<style>
v-toolbar__content,
.v-toolbar__extension {
    align-items: start !important;
    padding: 0;
}

.v-avatar {
    height: 15px !important;
    min-width: 15px !important;
    width: 15px !important;
    margin: 0 0.2rem;
}

.blue-gradient {
    background: linear-gradient(to bottom, #5fb5f2, #0798ff);
    border: solid 2px #fff;
    height: 50px !important;
    min-width: 50px !important;
    width: 50px !important;
}

.yellow-gradient {
    background: linear-gradient(to bottom, #f2c45f, #ffc107);
}

.green-gradient {
    background: linear-gradient(to bottom, #81f25f, #5eff07);
}

.red-gradient {
    background: linear-gradient(to bottom, #722b2b, #8b0404);
}

@keyframes redblink {
    50% {
        background: #804646;
        border: solid 2px #8b0404;
    }
}

@keyframes yellowblink {
    50% {
        background: #fbd564;
        border: solid 2px #ffc107;
    }
}

@keyframes greenblink {
    50% {
        background: #b0f28c;
        border: solid 2px #5eff07;
    }
}

.blinking-red {
    animation: redblink 2s infinite;
}

.blinking-yellow {
    animation: yellowblink 3s infinite;
}

.blinking-green {
    animation: greenblink 4s infinite;
}

.menu-bar {
    position: relative !important;
    flex: none;
    color: #fff;
}

.text-decoration-none {
    text-decoration: none;
}
</style>