<template>
    <v-container>
        <v-card>
            <v-tabs v-model="tab" bg-color="primary">
                <v-tab value="one" color="yellow">Componentes Vuetify</v-tab>
                <v-tab value="two" color="yellow">Componentes simples</v-tab>
                <v-tab value="three" color="yellow">Item Three</v-tab>

            </v-tabs>

            <v-card-text>
                <v-tabs-window v-model="tab">
                    <v-tabs-window-item value="one">
                        <h1 class="mb-8">Componente Vuetify</h1>
                        <v-row>
                            <v-col cols="12" xs="12" sm="8" md="4" lg="4" xl="4">
                                <ValidaCepVuetify />
                            </v-col>
                        </v-row>
                    </v-tabs-window-item>

                    <v-tabs-window-item value="two">
                    </v-tabs-window-item>

                    <v-tabs-window-item value="three">
                        Three
                    </v-tabs-window-item>
                </v-tabs-window>
            </v-card-text>
        </v-card>
    </v-container>
</template>


<script>
import ValidaCepVuetify from '../components/vuetify/ValidaCepVuetify.vue'
export default {
    components: {
        ValidaCepVuetify
    },
    data() {
        return {
            tab: 'one'
        }
    }
}

</script>

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