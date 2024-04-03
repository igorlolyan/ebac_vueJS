<script setup>
  import { ref } from 'vue';

  const num1 = ref(0);
  const num2 = ref(0);
  const selectedOperation = ref('Soma');

  const calcular = () => {
    let resultado;
    switch (selectedOperation.value) {
      case 'Soma':
      resultado = parseInt(num1.value) + parseInt(num2.value);
        break;
      case 'Subtração':
        resultado = num1.value - num2.value;
        break;
      case 'Multiplicação':
        resultado = num1.value * num2.value;
        break;
      case 'Divisão':
        resultado = num1.value / num2.value;
        break;
      default:
        resultado = 'Operação inválida';
    }
    return resultado;
  };
</script>

<template>
  <header>
    <input type="text" v-model="num1">
    <input type="text" v-model="num2">
    <label>
      Escolha:
      <select v-model="selectedOperation">
        <option value="Soma">Soma</option>
        <option value="Subtração">Subtração</option>
        <option value="Multiplicação">Multiplicação</option>
        <option value="Divisão">Divisão</option>
      </select>
    </label>
    <p class="result">Resultado: {{ calcular() }}</p>
  </header>
</template>

<style scoped>
header {
  background-color: #f8f9fa;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

input[type="text"] {
  padding: 10px;
  font-size: 16px;
  border-radius: 5px;
  border: 1px solid #ced4da;
  margin-right: 10px;
}

select {
  padding: 10px;
  font-size: 16px;
  border-radius: 5px;
  border: 1px solid #ced4da;
  margin-right: 10px;
}

.result {
  font-size: 30px;
  margin-top: 20px;
}
</style>