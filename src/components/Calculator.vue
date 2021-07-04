<template>
  <div class="calulator">
    <div class="display">{{ firstNum + currentNum }}</div>

    <div class="answer">
      <span v-if="checkEqual">=</span>
      {{ +result }}
    </div>
    <div class="body-calulator">
      <div>
        <button @click="reset">C</button>
        <button @click="percent">%</button>
        <button @click="invert">+/-</button>
        <button @click="divide('/')">/</button>
      </div>
      <div>
        <button @click="input('7')">7</button>
        <button @click="input('8')">8</button>
        <button @click="input('9')">9</button>
        <button @click="plus('+')">+</button>
      </div>
      <div>
        <button @click="input('4')">4</button>
        <button @click="input('5')">5</button>
        <button @click="input('6')">6</button>
        <button @click="multiply('*')">X</button>
      </div>
      <div>
        <button @click="input('1')">1</button>
        <button @click="input('2')">2</button>
        <button @click="input('3')">3</button>
        <button @click="minus('-')">-</button>
      </div>

      <div>
        <button @click="input('0')">0</button>
        <button @click="input('.')">.</button>
        <button @click="equal('=')">=</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  //initial
  data() {
    return {
      firstNum: "",
      currentNum: "",
      result: "",
      percentPre: "",
      checkEqual: false,
    };
  },
  methods: {
    input(num) {
      this.currentNum += num;
    },
    plus(operator) {
      this.firstNum += this.currentNum + operator;
      this.currentNum = "";
    },
    minus(operator) {
      this.firstNum += this.currentNum + operator;
      this.currentNum = "";
    },
    multiply(operator) {
      this.firstNum += this.currentNum + operator;
      this.currentNum = "";
    },
    divide(operator) {
      this.firstNum += this.currentNum + operator;
      this.currentNum = "";
    },
    percent() {
      if (
        this.firstNum.charAt(this.firstNum.length - 1) == "*" ||
        this.firstNum.charAt(this.firstNum.length - 1) == "/"
      ) {
        this.currentNum = this.currentNum / 100;
      }
      this.percentPre = (this.firstNum.slice(0, -1) * this.currentNum) / 100;
      this.firstNum += this.percentPre;
      this.currentNum = "";
    },
    equal() {
      if (this.firstNum == "") {
        this.result = 0;
      } else {
        this.result = eval(this.firstNum + this.currentNum);
        this.checkEqual = true;
      }
    },
    reset() {
      this.firstNum = "";
      this.currentNum = "";
      this.result = "";
      this.checkEqual = false;
    },
    invert() {
      this.currentNum =
        this.currentNum.charAt(0) == "-"
          ? this.currentNum.slice(1)
          : `- ${this.currentNum}`;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calulator {
  background: #f8f8f8;
  border: solid #bdbdbd 1px;
  box-shadow: 1px 1px 6px rgba(0, 0, 0, 0.5);
  -webkit-box-shadow: 1px 1px 6px rgba(0, 0, 0, 0.5);
  -moz-box-shadow: 1px 1px 6px rgba(0, 0, 0, 0.5);
  width: 27%;
  margin: 0 auto;
}
.body-calulator div {
  display: flex;
  justify-content: space-around;
}
.body-calulator button {
  width: 100%;
  background: #f3ccbd;
  margin: 15px;
  height: 60px;
  border: 1px solid #eeeeee;
}
.answer,
.display {
  height: 26px;
  text-align: right;
  padding: 13px 15px;
  font-size: 25px;
}
</style>
