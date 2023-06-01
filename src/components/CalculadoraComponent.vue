<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <table class="table table-bordered">
      <tbody>
        <tr class="resultado">
          <!-- Ocupa 4 tabelas no grid -->
          <td colspan="4">{{output || 0}}</td>
        </tr>
        <tr class="operadores">
          <td @click="clearField">C</td>
          <td @click="setNegativeOrPositive">+/-</td>
          <td @click="percentage">%</td>
          <td @click="processOperation('divide')">/</td>
        </tr>
        <tr class="operadores">
          <td class="numbers" v-on:click="getNumber('7')">7</td>
          <td class="numbers" v-on:click="getNumber('8')">8</td>
          <td class="numbers" v-on:click="getNumber('9')">9</td>
          <td class="operadores" v-on:click="processOperation('multiply')">x</td>
        </tr>
        <tr class="operadores">
          <td class="numbers" v-on:click="getNumber('4')">4</td>
          <td class="numbers" v-on:click="getNumber('5')">5</td>
          <td class="numbers" v-on:click="getNumber('6')">6</td>
          <td class="operadores" v-on:click="processOperation('minus')">-</td>
        </tr>
        <tr class="operadores">
          <td class="numbers" v-on:click="getNumber('1')">1</td>
          <td class="numbers" v-on:click="getNumber('2')">2</td>
          <td class="numbers" v-on:click="getNumber('3')">3</td>
          <td class="operadores" v-on:click="processOperation('plus')">+</td>
        </tr>
        <tr>
          <td colspan="2" class="numbers" v-on:click="getNumber('0')">0</td>
          <td class="numbers" v-on:click="getDot">.</td>
          <td class="operadores" v-on:click="updateOutput" @keypress.enter.prevent="updateOutput">=</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'CalculadoraComponent',
  props: {
    msg: String
  },
  data(){
    return{
      output: '',
      previousValue: null,
      operationFired: false
    } 
  },
  methods:{
    clearField(){
      this.output = '';
    },
    percentage(){
      this.output = parseFloat(this.output)/100; 
    },
    setNegativeOrPositive(){
      this.output = this.output[0] === '-' ? this.output.slice(1) : `${-this.output}`;
    },
    getNumber(number){
      if(this.operationFired){
        this.output = '';
        this.operationFired = false;
      }
      this.output = `${this.output}${number}`;
    },
    getDot(){
      if(this.output.indexOf('.') === -1){
        this.output = this.output + '.';
      }
    },
    processOperation(operation){
      if(operation === 'plus'){
        this.operation = (a, b) => {
          return parseFloat(a) + parseFloat(b);
        }
      } else if(operation === 'minus'){
        this.operation = (a, b) => {
          return parseFloat(a) - parseFloat(b);
        }
      } else if(operation === 'multiply'){
        this.operation = (a, b) => {
          return parseFloat(a) * parseFloat(b);
        }
      } else if(operation === 'divide'){
        this.operation = (a, b) => {
          return parseFloat(a) / parseFloat(b);
        }
      }
      this.previousValue = this.output;
      this.operationFired = true;
    },
    updateOutput(){
      this.output = `${this.operation(this.previousValue, this.output)}`;
      this.previousValue = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.operadores{
  background-color: rgb(190, 190, 190);
}
.numbers{
  background-color: white;
}
.resultado{
  background-color: #42b983;
}
td:active{
  background-color: gray;
}
</style>
