<script setup>
import ValidaCpf from '../components/ValidaCpf.vue'
import ValidaCnpj from '../components/ValidaCnpj.vue'
import ValidaCep from '../components/ValidaCep.vue'
import { ref } from 'vue'
const tab = ref('one')  
</script>

<template>
    <v-container>
        <v-card>
            <v-tabs v-model="tab" bg-color="primary">
                <v-tab value="one" color="yellow">Componentes simples</v-tab>
                <v-tab value="two" color="yellow">Item Two</v-tab>
                <v-tab value="three" color="yellow">Item Three</v-tab>
            </v-tabs>

            <v-card-text>
                <v-tabs-window v-model="tab">
                    <v-tabs-window-item value="one">
                        <h1>Componentes de validação em formularios</h1>
                        <h2>Componentes simples apenas html css</h2>
                        <hr>
                        <ValidaCpf />
                        <hr>
                        <ValidaCnpj />
                        <hr>
                        <ValidaCep />
                    </v-tabs-window-item>

                    <v-tabs-window-item value="two">
                        Two
                    </v-tabs-window-item>

                    <v-tabs-window-item value="three">
                        Three
                    </v-tabs-window-item>
                </v-tabs-window>
            </v-card-text>
        </v-card>
    </v-container>
</template>

<style scoped>
.main {
    padding: 20px;
    width: 100%;
}

hr {
    margin: 20px 0;
    border: 0;
    border-top: 1px solid #ccc;
}
</style>