<template>
    <div>
      <form @submit.prevent="checkCpf">
        <div class="form-group">
          <label for="cpf">CPF</label><br>
          <input
            id="cpf"
            v-model="formattedCpf"
            v-on:input="formatCpf"
            placeholder="000.000.000-00"
            maxlength="14"
          >
          <br>
          <span v-if="error" class="error">{{ error }}</span>
        </div>
        <button type="submit">Verificar CPF</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        cpf: '',
        error: ''
      };
    },
    computed: {
      formattedCpf: {
        get() {
          return this.cpf.replace(/\D/g, '').replace(/(\d{3})(\d{3})(\d{3})(\d{2})/, '$1.$2.$3-$4');
        },
        set(value) {
          this.cpf = value.replace(/\D/g, '');
        }
      }
    },
    methods: {
      formatCpf(event) {
        let value = event.target.value.replace(/\D/g, '');
        value = value.replace(/(\d{3})(\d{3})(\d{3})(\d{2})/, '$1.$2.$3-$4');
        this.cpf = value;
      },
      validateCpf() {
        let cleanedCpf = this.cpf.replace(/\D/g, '');
  
        if (cleanedCpf.length !== 11 || /^(.)\1{10}$/.test(cleanedCpf)) {
          this.error = 'CPF inválido';
          return false;
        }
  
        let sum = 0;
        let remainder;
        for (let i = 1; i <= 9; i++) {
          sum += parseInt(cleanedCpf.substring(i - 1, i)) * (11 - i);
        }
        remainder = (sum * 10) % 11;
  
        if (remainder === 10 || remainder === 11) {
          remainder = 0;
        }
  
        if (remainder !== parseInt(cleanedCpf.substring(9, 10))) {
          this.error = 'CPF inválido';
          return false;
        }
  
        sum = 0;
        for (let i = 1; i <= 10; i++) {
          sum += parseInt(cleanedCpf.substring(i - 1, i)) * (12 - i);
        }
        remainder = (sum * 10) % 11;
  
        if (remainder === 10 || remainder === 11) {
          remainder = 0;
        }
  
        if (remainder !== parseInt(cleanedCpf.substring(10, 11))) {
          this.error = 'CPF inválido';
          return false;
        }
  
        this.error = '';
        return true;
      },
      checkCpf() {
        if (this.validateCpf()) {
          alert('CPF válido!');
        }
      }
    }
  };
  </script>
  
  <style>
  .form-group {
    margin-bottom: 20px;
  }
  .error {
    color: red;
    font-size: 0.8em;
  }
  </style>
  