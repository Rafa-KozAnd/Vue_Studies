<template>
  <div id="app">
    <h1>Simulador de Investimentos</h1>
    
    <div>
      <label for="initialAmount">Valor Inicial:</label>
      <input v-model.number="initialAmount" type="number" placeholder="Valor inicial" />
    </div>
    
    <div>
      <label for="interestRate">Taxa de Juros Mensal (%):</label>
      <input v-model.number="interestRate" type="number" placeholder="Taxa de juros" />
    </div>
    
    <div>
      <label for="months">Meses:</label>
      <input v-model.number="months" type="number" placeholder="Número de meses" />
    </div>
    
    <button @click="calculateInvestment">Calcular Investimento</button>
    
    <div v-if="calculatedAmount !== null">
      <h2>Resultado</h2>
      <p>Valor Final após {{ months }} meses: R$ {{ calculatedAmount.toFixed(2) }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      initialAmount: 0,
      interestRate: 0,
      months: 0,
      calculatedAmount: null
    };
  },
  methods: {
    calculateInvestment() {
      const rate = this.interestRate / 100;
      this.calculatedAmount = this.initialAmount * Math.pow(1 + rate, this.months);
    }
  }
};
</script>

<style scoped>
label {
  margin-right: 10px;
}
input {
  margin-bottom: 10px;
  padding: 5px;
}
button {
  margin-top: 10px;
  padding: 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}
button:hover {
  background-color: #45a049;
}
</style>
