<script setup>
import ValidaCpf from '../components/ValidaCpf.vue'
import ValidaCnpj from '../components/ValidaCnpj.vue'
import ValidaCep from '../components/ValidaCep.vue'
</script>

<template>
    <div class="main">
        <h1>Componentes de validação em formularios</h1>
        <h2>Componentes simples apenas html css</h2>
        <hr>
        <ValidaCpf />
        <hr>
        <ValidaCnpj />
        <hr>
        <ValidaCep />
    </div>
</template>

<style scoped>
.main {
    padding: 20px;
    width: 100vw;
}
hr {
    margin: 20px 0;
    border: 0;
    border-top: 1px solid #ccc;
}

</style>