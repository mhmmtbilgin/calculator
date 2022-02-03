<template>
  <div>
    <h2>Basic Calculator</h2>
    <div class="calculator">
      <div class="screen">{{ current || "0" }}</div>
      <div @click="clearScreen" class="btn">C</div>
      <div @click="sign" class="btn">+/-</div>
      <div @click="percent" class="btn">%</div>
      <div @click="divide" class="btn operator">/</div>
      <div @click="append('7')" class="btn">7</div>
      <div @click="append('8')" class="btn">8</div>
      <div @click="append('9')" class="btn">9</div>
      <div @click="times" class="btn operator">x</div>
      <div @click="append('4')" class="btn">4</div>
      <div @click="append('5')" class="btn">5</div>
      <div @click="append('6')" class="btn">6</div>
      <div @click="minus" class="btn operator">-</div>
      <div @click="append('1')" class="btn">1</div>
      <div @click="append('2')" class="btn">2</div>
      <div @click="append('3')" class="btn">3</div>
      <div @click="add" class="btn operator">+</div>
      <div @click="append('0')" class="zero btn">0</div>
      <div @click="dot" class="btn">.</div>
      <div @click="equals" class="btn operator">=</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorClicked: false,
    };
  },
  methods: {
    clearScreen() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current / 100)}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      if (this.current !== "0") {
        this.current = `${this.current}${number}`;
      }
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrev() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrev();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrev();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrev();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrev();
    },
    equals() {
      this.current = this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      );
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  margin: 0 auto;
  width: 300px;
  font-size: 30px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  box-shadow: -3px 4px #eee;
}
.screen {
  display: grid;
  justify-content: flex-end;
  align-items: flex-end;
  grid-column: 1 / 5;
  padding: 0 15px;
  background-color: #333;
  color: white;
}
.zero {
  grid-column: 1/3;
}
.btn {
  background-color: #f2f2f2;
  border: 1px solid #999;
}
.operator {
  background-color: orange;
  color: white;
}
</style>
