<template>
<div class="main">
<h1 class="heading">Calculator</h1>

<div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="divide">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="times">×</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append(6)">6</div>
    <div class="btn operator" @click="minus">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="add">+</div>
    <div class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="equal">=</div>
</div>




</div>
</template>

<script>
export default {
data(){
    return{
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
      result: null
      
    }
},
methods:{
    clear(){
     this.current = ''
    },
    sign(){
        this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
    },
    percent(){
        this.current = `${parseFloat(this.current) / 100}`
    },
    append(number){
        if(this.operatorClicked){
            this.current = '';
            this.operatorClicked = false;
        } else if(this.result === this.current){
            this.current = ''
        }
            this.current = `${this.current}${number}`;
        
    },
    dot(){
        if(this.current.indexOf('.') === -1){
            this.append('.');
        }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide(){
        this.operator = (a, b) => a / b;
        this.setPrevious();
    },
    times(){
        this.operator = (a, b) => a * b;
        this.setPrevious();
    },
    minus(){
        this.operator = (a, b) => a - b;
        this.setPrevious();
    },
    add(){
        this.operator = (a, b) => a + b;
        this.setPrevious();
    },
    equal(){
       this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`;
       return this.result = this.current
       this.previous = null
    }
}
}
</script>

<style scoped>
.heading{
    margin-left: 140px;
}
.calculator {
 margin-left: 30px;
 width: 400px;
 display: grid;
 grid-template-columns: repeat(4, 1fr);
 grid-auto-rows: minmax(50px, auto);
}

.display {
   grid-column: 1/5;
   background-color: rgb(175, 174, 174);
   text-align: right;
   color: white;
   font-size: 30px;
   padding: 10px
}

.zero {
 grid-column: 1/3;
 text-align: center;
}

.btn{
    padding: 10px;
    background-color: rgb(247, 243, 243);
    border: 0.5px solid rgb(150, 148, 148);
    font-size: 20px;
}

.operator{
    background-color: orange;
    color: white
}
</style>