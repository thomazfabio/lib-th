<script>
export default {
    name: "ValidaCepVuetify",
    data: () => ({
        loaded: false,
        loading: false,
    }),

    methods: {
        onClick() {
            this.loading = true

            setTimeout(() => {
                this.loading = false
                this.loaded = true
            }, 2000)
        },
    },
}
</script>

<template>
    <v-text-field :loading="loading" append-inner-icon="mdi-magnify" density="compact" label="CEP" variant="outlined"
        hide-details @click:append-inner="onClick"></v-text-field>
</template>