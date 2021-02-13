<template>
<div id="app">

  <div class="main-wrapper animate__animated animate__zoomIn">
    <div class="screen">
      <div class="res">{{ current }}</div>
    </div>
    <div class="number-wrapper">
      <div @click="clear()" class="num">AC</div>
      <div @click="sign()" class="num">+/-</div>
      <div @click="persent()" class="num">%</div>
      <div @click="devide()" class="num orange">/</div>
      <div @click="append('7')" class="num">7</div>
      <div @click="append('8')" class="num">8</div>
      <div @click="append('9')" class="num">9</div>
      <div @click="multiply()" class="num orange">*</div>
      <div @click="append('4')" class="num">4</div>
      <div @click="append('5')" class="num">5</div>
      <div @click="append('6')" class="num">6</div>
      <div @click="abstr()" class="num orange">-</div>
      <div @click="append('1')" class="num">1</div>
      <div @click="append('2')" class="num">2</div>
      <div @click="append('3')" class="num">3</div>
      <div @click="add()" class="num orange">+</div>
      <div @click="append('0')" class="num orange zero">0</div>
      <div @click="dot()" class="num orange">.</div>
      <div @click="res()" class="num orange equal">=</div>
    </div>
  </div>

</div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return {
      prevNumber: null,
      clicked: false,
      operator: null,
      current: '',
      result: ''
    }
  },
  methods: {
    clear(){
      this.current = '';
    },
    sign(){
      this.current = this.current[0] === '-' ? this.current.slice(1) : `-${this.current}`;
    },
    persent(){
      this.current = eval(this.current / 100);
    },
    append(number){
      this.current = `${this.current}${number}`;
    },
    dot(){
      this.current = !/[.]/g.test(this.current) ? `${this.current}.` : this.current;
    },
    devide(){
      this.operator = (x,y) => x / y;
      this.prevNumber = this.current;
      this.current = '';
    },
    multiply(){
      this.operator = (x,y) => x * y;
      this.prevNumber = this.current;
      this.current = '';
    },
    abstr(){
      this.operator = (x,y) => x - y;
      this.prevNumber = this.current;
      this.current = '';
    },
    add(){
      this.operator = (x,y) => x + y;
      this.prevNumber = this.current;
      this.current = '';
    },
    res(){
     this.current= `${this.operator(
        parseFloat(this.prevNumber),
        parseFloat(this.current)
      )}`;
    }
  }
}
</script>

<style lang="scss">

body {
  display: flex;
  justify-content: center;
  padding-top: 150px;
  .main-wrapper {
    background-color: #E1E1E0;
    width: 250px;
    border-radius: 10px;
    box-shadow: 10px 15px 25px gray;
    .screen {
      width: 100%;
      height: 75px;
      color: lightgray;
      border-radius: 10px 10px 0 0;
      background-color: rgba(0, 0, 0, 0.6);
      .res {
        float: right;
        font-size: 40px;
        padding: 20px 15px 0 0;
      }
    }
      .number-wrapper {
        display: grid;
        grid-template-columns: repeat(4,62.5px);
        grid-template-rows: repeat(4,auto);
        text-align: center;
        font-size: 25px;
        cursor: pointer;
        .num {
          padding: 5px;
          border: 1px solid gray;
        }
        .zero {
          grid-column: 1/3;
          border-radius: 0 0 0 10px;
        }
        .equal {
          border-radius: 0 0 9px 0;
        }
        .orange {
          background-color: #F79232;
        }
    }
  }
}
</style>
