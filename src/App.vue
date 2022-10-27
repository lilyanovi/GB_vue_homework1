<template>
  <div id="app" class="center">
    <h1>Калькулятор</h1>
    <input v-on:click="activateOperand(1)" type="number" v-model="operand1">
    <input v-on:click="activateOperand(2)" type="number" v-model="operand2">

    <p>Операнд {{ activeOperand }}</p>
    <p>Результат: {{ result }}</p>

    <div v-if="error" class="error">{{ error }}</div>
   
    <button v-for="item, index of operations" v-bind:key="index" v-on:click="currentOperation = item">{{ item }}</button>

    <label class="keyboard">
      <input type="checkbox" v-model="checked">
    Отобразить экранную клавиатуру
    </label>
    <div v-if="checked">
      <button v-for="item, index of numbers" v-bind:key="index" @click="interNumber(item)">{{ item }}</button>
      <button @click="clear">&#8592;</button>
    </div>

    <ul>
      <li v-for="item, index of logList" v-bind:key="index">{{ item }}</li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: "App",
    data () {
      return {
        activeOperand: 1,
        operand1: "0",
        operand2: "0",
        currentOperation: "+",
        error: "",
        operations: [
          '+',
          '-',
          '/',
          '*',
          'Возведение в степень',
          'Целочисленное деление'
        ],
        numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
        logList:[],
        checked: ""
      }
    },
    computed:{
      result() {
        return this.doCalc(this.currentOperation)
      }
    },
    methods: {
      interNumber(item) {
        if(this.activeOperand == 1) {
          this.operand1 += item
        } else {
          this.operand2 += item
        }
      },
      clear(){
        if(this.activeOperand == 1) {
          this.operand1 = this.operand1.slice(0,-1)
        } else {
          this.operand2 = this.operand2.slice(0,-1)
        }
      },
      activateOperand(id){
        this.activeOperand = id
      },
      sum() {
        return Number(this.operand1) + Number(this.operand2)
      },
      subtract() {
        return Number(this.operand1) - Number(this.operand2)
      },
      division() {
        if(Number(this.operand2 == 0))  {
          this.error = 'На ноль делить нельзя'
          return
        }
        return Number(this.operand1) / Number(this.operand2)
      },
      multiply() {
        return Number(this.operand1) * Number(this.operand2)
      },
      exponentiation() {
        return Math.pow(Number(this.operand1), Number(this.operand2))
      },
      integer() {
        return Math.floor(Number(this.operand1) / Number(this.operand2))
      },
      doCalc(operator){
        this.error =''
        this.logList.push(`${new Date().toDateString()}: ${this.operand1} ${operator} ${this.operand2}`)
        switch (operator){
          case "+":
            return this.sum()
            break;
          case "-":
          return this.subtract()
            break;
          case "/":
            return this.division()
            break;
          case "*":
            return this.multiply()
            break;
          case "Возведение в степень":
            return this.exponentiation()
            break;
          case "Целочисленное деление":
            return this.integer()
            break;
          default:
            return this.result = 'Error'
            break;
        
        }
      }
    }
  }
</script>

<style lang="scss">
.center {
    padding-left: calc(50% - 570px);
    padding-right: calc(50% - 570px);
}
.error {
    color: darkred;
    border: solid 1px darkred;
    margin: 10px 0;
    padding: 10px 20px;
    display: block;
}
.keyboard {
    display: block;
    margin-top: 20px;
}
</style>
