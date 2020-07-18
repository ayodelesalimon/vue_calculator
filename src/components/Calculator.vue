<template>

  <div class="body">
      <div class="h1">Simple Calculator With Vue</div>
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn">AC</div>
    <div @click="sign" class="btn">-/+</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="substract" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>

    <footer class="footer">Made with ❤️ by <a href="http://github.com/ayodelesalimon">Ayodele Salimonu</a></footer>
  </div>

</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current)}` / 100;
    },

    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
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
      this.current = `${this.operator(parseFloat(this.current), parseFloat(this.previous))}`;
      this.previous = null;
    }
  }
};
</script>

<style scoped>

.body {
    
  width: 400px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.h1{
    grid-column: 1/5;
    font-size: 30px;
}
.display {
  text-align: right;
  font-size: 29px;
  grid-column: 1/5;
  color: white;
  background-color: #333;
}
.zero {
  grid-column: 1/3;
}
.btn {
  font-size: 30px;
  background-color: #eee;
  border: 1px solid #999;
}
.operator {
  background-color: orange;
  color: white;
}
.footer{
    grid-column: 1/5;
}
.footer a{
    text-decoration: none;
}

</style>
