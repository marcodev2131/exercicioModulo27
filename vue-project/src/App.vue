<template>
  <div id="app" class="container mt-5">
    <h1 class="text-center mb-4">Calculadora Aritmética</h1>
    <div class="form-group">
      <input 
        v-model.number="number1" 
        @input="validateNumber('number1')" 
        :class="{'is-invalid': number1Error}" 
        placeholder="Insira o primeiro número" 
        type="number" 
        class="form-control mb-2" 
      />
      <div class="invalid-feedback" v-if="number1Error">{{ number1Error }}</div>
      <select v-model="operation" class="form-control mb-2">
        <option value="add">+</option>
        <option value="subtract">-</option>
        <option value="multiply">*</option>
        <option value="divide">/</option>
      </select>
      <input 
        v-model.number="number2" 
        @input="validateNumber('number2')" 
        :class="{'is-invalid': number2Error}" 
        placeholder="Insira o segundo número" 
        type="number" 
        class="form-control mb-2" 
      />
      <div class="invalid-feedback" v-if="number2Error">{{ number2Error }}</div>
    </div>
    <h2 class="text-center mt-4">Resultado: {{ result }}</h2>
  </div>
</template>

<script>
export default {
  data() {
    return {
      number1: null,
      number2: null,
      operation: 'add',
      number1Error: null,
      number2Error: null,
    };
  },
  computed: {
    result() {
      if (this.number1Error || this.number2Error) {
        return 'Corrija os erros antes de prosseguir';
      }
      switch (this.operation) {
        case 'add':
          return this.number1 + this.number2;
        case 'subtract':
          return this.number1 - this.number2;
        case 'multiply':
          return this.number1 * this.number2;
        case 'divide':
          return this.number2 !== 0 ? this.number1 / this.number2 : 'Divisão por zero';
        default:
          return 0;
      }
    },
  },
  methods: {
    validateNumber(field) {
      if (field === 'number1') {
        this.number1Error = this.number1 === null ? 'O primeiro número é obrigatório' : null;
      } else if (field === 'number2') {
        if (this.number2 === null) {
          this.number2Error = 'O segundo número é obrigatório';
        } else if (this.operation === 'divide' && this.number2 === 0) {
          this.number2Error = 'Divisão por zero não é permitida';
        } else {
          this.number2Error = null;
        }
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
}
</style>
