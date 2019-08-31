<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="appendNum('7')" class="btn">7</div>
    <div @click="appendNum('8')" class="btn">8</div>
    <div @click="appendNum('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">X</div>
    <div @click="appendNum('4')" class="btn">4</div>
    <div @click="appendNum('5')" class="btn">5</div>
    <div @click="appendNum('6')" class="btn">6</div>
    <div @click="substract" class="btn operator">-</div>
    <div @click="appendNum('1')" class="btn">1</div>
    <div @click="appendNum('2')" class="btn">2</div>
    <div @click="appendNum('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="appendNum('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      current: "",
      previous: "",
      operator: "",
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      if (this.current === "" || this.current === "0") {
        return;
      }
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    appendNum(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      if ((this.current === "" || this.current === "0") && number === "0") {
        return;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.appendNum(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    substract() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.previous = "";
    }
  }
};
</script>

<style scoped>
.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}

.zero {
  grid-column: 1 / 3;
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
