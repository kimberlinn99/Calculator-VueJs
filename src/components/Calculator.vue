<template>
  <div class="calculator">
    <div class="display-previous">{{ previous }}</div>
    <div class="display-current">{{ current || 0 }}</div>
    <div class="btn special" @click="clear">AC</div>
    <div class="btn special" @click="plusMinusSign">+/-</div>
    <div class="btn special" @click="percent">%</div>
    <div class="btn operator" @click="operation('÷')">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="operation('x')">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="operation('-')">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="operation('+')">+</div>
    <div class="zero btn" @click="append('0')">0</div>
    <div class="btn" @click="append('.')">.</div>
    <div class="btn operator" @click="equal">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      previous: '',
      current: '',
      stringLength: 8
    }
  },
  methods: {
    append(number){
      if(number == '0' && this.current.charAt(0) == '0') return
      if(number == '.' && this.current.includes('.')) return
      this.current = `${this.current}${number}`
      this.checkLength()
    },
    clear(){
      this.current = ''
    },
    plusMinusSign(){
      if(this.current != ''){
        if(this.current.charAt(0) !== '-' && this.current.charAt(0) !== '0'){
          this.current = `- ${this.current}`
        }else{
          this.current = this.current.replace('-', '')
        }
      }
    },
    percent(){
      this.current = (parseFloat(this.current) / 100).toString()
      this.checkLength()
    },
    operation(operator){
      this.previous = `${this.current} ${operator}` 
      this.current = ''
    },
    equal(){
      if(this.current == '') return
      var operator = this.previous.split(' ')[1]
      var current = parseFloat(this.current)
      var previous = parseFloat(this.previous)
      switch(operator){
        case '+':
          this.current = previous + current
          this.current = this.current.toString()
          this.previous = '' 
          break;
        case '-':
          this.current = previous - current
          this.current = this.current.toString()
          this.previous = '' 
          break;
        case '÷':
          this.current = previous / current
          this.current = this.current.toString()
          this.previous = '' 
          break;
        case 'x':
          this.current = previous * current
          this.current = this.current.toString()
          this.previous = '' 
          break;
        default:
          this.previous = ''
          break;  
      }
      this.checkLength()
    },
    checkLength(){
      if(this.current.length > this.stringLength){
        this.current = this.current.substring(0,9)
      }
    }
  }
}
</script>

<style scoped>
.calculator{
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  width: 300px;
  grid-auto-rows: minmax(50px, auto);
  margin: 0 auto;
  font-size: 1.5em;
}
.display-previous, .display-current{
  grid-column: 1 / 5;
  background-color: black;
  color: aliceblue;
  padding: 5px 10px;
  text-align: end;
}
.display-current{
  font-size: 2em;
}
.btn{
  padding: 15px 0px;
  border: 0.5px solid rgb(22, 21, 21);
}
.btn:hover{
  cursor: pointer;
}
.zero{
  grid-column: 1/3;
}
.operator{
  background-color: rgb(241, 161, 32);
  color: aliceblue;
}
.special{
  background-color: rgb(216, 216, 216);
}
</style>
