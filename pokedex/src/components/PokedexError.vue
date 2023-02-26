<template>
    <v-alert :value="show" style="background-color: transparent;">
        <v-container class="d-flex flex-column justify-center align-center">
            <a href="https://fontmeme.com/pt/fonte-de-pokemon/"><img style="max-width: 100%; height: auto; margin: 0 auto;"
                    src="https://fontmeme.com/permalink/230226/9a84799b6cc498489c25e08ecff1a3f2.png" alt="fonte-de-pokemon"
                    border="0"></a>
            <a href="https://fontmeme.com/pt/fonte-de-pokemon/"><img style="max-width: 100%; height: auto;"
                    src="https://fontmeme.com/permalink/230226/dc6bce53b818cda744c184aaf057d185.png" alt="fonte-de-pokemon"
                    border="0"></a>
        </v-container>
    </v-alert>
</template>
  
<script>
export default {
    name: "PokedexError",
    props: {
        message: {
            type: String,
            required: true,
        },
        show: {
            type: Boolean,
            default: false,
        },
    },
};
</script>

<style>
.error-message {
    background-color: #ffebee;
    border: 1px solid #ef9a9a;
    border-radius: 4px;
    padding: 8px;
    margin-bottom: 16px;
}
</style>