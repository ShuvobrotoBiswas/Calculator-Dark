<template>
  <div class="light">
    <Calculator msg="Calculator"/>
    <div class="calculator">
     <div  class="">Calculator</div> <br>
     <div class="display">{{current || '0'}}</div>
     <div @click="clear" class="btn1">C</div>
     <div @click="sign" class="btn1">+/-</div>
     <div @click="percent" class="btn1">%</div>
     <div @click="divide" class="btn operator">÷</div>
     <div @click="append('7')" class="btn">7</div>
     <div @click="append('8')" class="btn">8</div>
     <div @click="append('9')" class="btn">9</div>
     <div @click="times" class="btn operator">×</div>
     <div @click="append('4')" class="btn">4</div>
     <div @click="append('5')" class="btn">5</div>
     <div @click="append('6')" class="btn">6</div>
     <div @click="minus" class="btn operator">−</div>
     <div @click="append('1')" class="btn">1</div>
     <div @click="append('2')" class="btn">2</div>
     <div @click="append('3')" class="btn">3</div>
     <div @click="add" class="btn operator">+</div>
     <div @click="append('0')" class="btn zero">0</div>
     <div @click="dot" class="btn">.</div>
     <div @click="equal" class="equal" v-on:click="getData()">=</div>
    
  </div>

  </div>
</template>

<script>
import Calculator from '@/components/Calculator.vue'

export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ?
      this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => b / a;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },
    methods:{
   getData(){
   this.$router.push('/History.vue'); 
      
      this.$router.push({name:'History.vue', params: {id: '[paramdata]'}});
      console.warn("values : this.equal");
   }
  },
  component: Calculator
  
  }
}
</script>


<!-- Calculator--- JS Ended  -->

<!-- Calculator--- CSS Started  -->
<style scoped>
.calculator {
  padding: 20px;
  margin: 0 auto;
  width: 600px;
  font-size: 40px;
  display: grid;
  border: 5px solid rgb(255, 102, 0);
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  background:white;
}
.display {
  padding: 20px;
  grid-column: 1/5;
  background-color: white;
  border: 15px solid rgb(255, 102, 0);
  text-align: right;
}
.zero {
  grid-column: 1 / 3;
}
.btn {
  padding: 30px;
  cursor: pointer;
  background-color: white;
  border: 1px solid #333;
  border-radius: 12px
  
}
.equal {
  padding: 30px;
  cursor: pointer;
  background-color: rgb(255, 102, 0);
  color: white;
  border: 1px solid rgb(255, 102, 0);
  border-radius: 100%
}
.operator {
  cursor: pointer;
  background-color: white;
  color: rgb(255, 102, 0);
}
.btn1 {
  padding: 30px;
  cursor: pointer;
  background-color: white;
  color: rgb(255, 102, 0);
  border: 1px solid #333;
  border-radius: 12px
}
</style>
