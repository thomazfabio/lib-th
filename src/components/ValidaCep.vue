<template>
    <div>
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label for="cep">CEP:</label>
          <input
            id="cep"
            v-model="cep"
            placeholder="00000-000"
            maxlength="9"
          >
        </div>
        <button type="submit">Enviar</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        cep: ''
      };
    },
    computed: {
      formattedCep() {
        let value = this.cep.replace(/\D/g, '');
        return value.replace(/^(\d{5})(\d{3})$/, '$1-$2');
      }
    },
    watch: {
      formattedCep(newVal) {
        this.cep = newVal;
      }
    },
    methods: {
      submitForm() {
        // Aqui você pode enviar o CEP para a API ou fazer o que desejar
        console.log('CEP enviado:', this.cep);
      }
    }
  };
  </script>
  
  <style>
  .form-group {
    margin-bottom: 20px;
  }
  </style>
  