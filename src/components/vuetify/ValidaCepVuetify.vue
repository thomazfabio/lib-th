<script>
import axios from 'axios'
export default {
    name: "ValidaCepVuetify",
    data: () => ({
        loaded: false,
        loading: false,
        cepDigitado: '',
    }),

    methods: {
        onClick() {
            this.loading = true
            const cep = this.cepDigitado.replace(/\D/g, '')
            //faz uma requisição para a API do viacep
            axios.get('https://viacep.com.br/ws/' + cep + '/json/')
                .then(response => {
                    console.log(response.data)
                    //aqui é feito a atribuição do resultado da requisição
                    this.loaded = response.data

                    this.loading = false
                })
                .catch(error => {
                    console.log(error)
                    //caso ocorra um erro, o loading é desativado e a mensagem de erro é exibida
                    this.loaded = { erro: true }
                    this.loading = false
                })
        },
    },
}
</script>

<template>
    <v-text-field v-model="cepDigitado" :loading="loading" append-inner-icon="mdi-magnify" density="compact" label="CEP" variant="outlined"
        hide-details @click:append-inner="onClick"> </v-text-field>
    <v-row v-if="loading">
        <v-col cols="12">
            <v-progress-linear indeterminate color="primary"></v-progress-linear>
        </v-col>
    </v-row>
    <v-row v-else-if="loaded">
        <v-col cols="12">
            <v-alert type="success" outlined>
                <h2>CEP: {{ loaded.cep }}</h2>
                <h2>Logradouro: {{ loaded.logradouro }}</h2>
                <h2>Bairro: {{ loaded.bairro }}</h2>
                <h2>Cidade: {{ loaded.localidade }}</h2>
                <h2>Estado: {{ loaded.uf }}</h2>
            </v-alert>
        </v-col>
    </v-row>
</template>