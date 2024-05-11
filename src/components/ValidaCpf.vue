<template>
    <div>
      <div>
        <label for="cpf">CPF:</label>
        <input type="text" id="cpf" v-model="cpf" @blur="validateCpf">
        <p v-if="error" style="color: red;">{{ error }}</p>
      </div>
      <div>
        <button @click="checkCpf">Verificar CPF</button>
      </div>
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
    methods: {
      validateCpf() {
        let cpf = this.cpf.replace(/[^\d]+/g, ''); // Remove caracteres não numéricos
        if (cpf.length !== 11 || /^(\d)\1{10}$/.test(cpf)) {
          this.error = 'CPF inválido';
          return false;
        }
        
        let sum = 0;
        let remainder;
        for (let i = 1; i <= 9; i++) {
          sum += parseInt(cpf.substring(i - 1, i)) * (11 - i);
        }
        remainder = (sum * 10) % 11;
        
        if ((remainder === 10) || (remainder === 11)) {
          remainder = 0;
        }
        
        if (remainder !== parseInt(cpf.substring(9, 10))) {
          this.error = 'CPF inválido';
          return false;
        }
        
        sum = 0;
        for (let i = 1; i <= 10; i++) {
          sum += parseInt(cpf.substring(i - 1, i)) * (12 - i);
        }
        remainder = (sum * 10) % 11;
        
        if ((remainder === 10) || (remainder === 11)) {
          remainder = 0;
        }
        
        if (remainder !== parseInt(cpf.substring(10, 11))) {
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
  