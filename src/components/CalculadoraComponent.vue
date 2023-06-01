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
          <td v-on:click="clearField">C</td>
          <td>&lt;</td>
          <td @click="percentage">%</td>
          <td>/</td>
        </tr>
        <tr class="operadores">
          <td class="numbers">7</td>
          <td class="numbers">8</td>
          <td class="numbers">9</td>
          <td class="operadores">x</td>
        </tr>
        <tr class="operadores">
          <td class="numbers">4</td>
          <td class="numbers">5</td>
          <td class="numbers">6</td>
          <td class="operadores">-</td>
        </tr>
        <tr class="operadores">
          <td class="numbers">1</td>
          <td class="numbers">2</td>
          <td class="numbers">3</td>
          <td class="operadores">+</td>
        </tr>
        <tr>
          <td colspan="2" class="numbers">0</td>
          <td class="numbers">.</td>
          <td class="operadores">=</td>
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
      output: '80'
    } 
  },
  methods:{
    clearField(){
      this.output = '0';
    },
    percentage(){
      this.output /= 100; 
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.operadores{
  background-color: black;
  color: orangered;
}
.numbers{
  background-color: rgb(32, 32, 32);
  color: white;
}
.resultado{
  background-color: rgb(32, 32, 32);
  color: orange;
}
td:active{
  background-color: gray;
}
</style>
