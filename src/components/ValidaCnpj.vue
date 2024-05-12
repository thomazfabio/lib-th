<template>
    <div>
      <form @submit.prevent="checkCnpj">
        <div class="form-group">
          <label for="cnpj">CNPJ</label><br>
          <input
            id="cnpj"
            v-model="cnpj"
            placeholder="00.000.000/0000-00"
            maxlength="18"
          >
          <br>
          <span v-if="error" class="error">{{ error }}</span>
        </div>
        <button type="submit">Verificar CNPJ</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        cnpj: '',
        error: ''
      };
    },
    computed: {
      formattedCnpj() {
        let value = this.cnpj.replace(/\D/g, '');
        return value.replace(/^(\d{2})(\d{3})(\d{3})(\d{4})(\d{2})$/, '$1.$2.$3/$4-$5');
      }
    },
    watch: {
      formattedCnpj(newVal) {
        this.cnpj = newVal;
      }
    },
    methods: {
      validateCnpj() {
        let cleanedCnpj = this.cnpj.replace(/\D/g, '');
  
        if (cleanedCnpj.length !== 14 || /^(.)\1{13}$/.test(cleanedCnpj)) {
          this.error = 'CNPJ inválido';
          return false;
        }
  
        let sum = 0;
        let length = cleanedCnpj.length - 2;
        let numbers = cleanedCnpj.substring(0, length);
        let digits = cleanedCnpj.substring(length);
        let pos = length - 7;
  
        for (let i = length; i >= 1; i--) {
          sum += numbers.charAt(length - i) * pos--;
          if (pos < 2) {
            pos = 9;
          }
        }
  
        let result = sum % 11 < 2 ? 0 : 11 - sum % 11;
  
        if (result != digits.charAt(0)) {
          this.error = 'CNPJ inválido';
          return false;
        }
  
        length = length + 1;
        numbers = cleanedCnpj.substring(0, length);
        sum = 0;
        pos = length - 7;
  
        for (let i = length; i >= 1; i--) {
          sum += numbers.charAt(length - i) * pos--;
          if (pos < 2) {
            pos = 9;
          }
        }
  
        result = sum % 11 < 2 ? 0 : 11 - sum % 11;
  
        if (result != digits.charAt(1)) {
          this.error = 'CNPJ inválido';
          return false;
        }
  
        this.error = '';
        return true;
      },
      checkCnpj() {
        if (this.validateCnpj()) {
          alert('CNPJ válido!');
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
  