<template>
  <div id="app">
    <h1>Калькулятор</h1>
    <input type="number" v-model="operand1">
    <input type="number" v-model="operand2">
    <p>Результат: {{result}}</p>
   
    <button v-on:click="result = Number(operand1) + Number(operand2)">+</button>
    <button v-on:click="result = Number(operand1) - Number(operand2)">-</button>
    <button v-on:click="result = Number(operand1) / Number(operand2)">/</button>
    <button v-on:click="result = Number(operand1) * Number(operand2)">*</button>
    <button v-on:click="result = Math.pow(Number(operand1), Number(operand2))">Возведение в степень</button>
    <button v-on:click="result = Math.floor(Number(operand1) / Number(operand2))">Целочисленное деление</button>
  </div>
</template>

<script>
  export default {
    name: "App",
    data () {
      return {
        operand1: "0",
        operand2: "0",
        result: "0"
      }
    }
  }
</script>

<style lang="scss">

</style>
