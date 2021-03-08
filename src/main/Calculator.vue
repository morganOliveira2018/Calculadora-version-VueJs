<template>
  <div class="calculator">
    <Display :value="displayValue" />
    <Button label="C" triple @onButtonClick="clearMemory" />
    <Button label="/" operation @onButtonClick="setOperation" />
    <Button label="7" @onButtonClick="addDigit" />
    <Button label="8" @onButtonClick="addDigit" />
    <Button label="9" @onButtonClick="addDigit" />
    <Button label="*" operation @onButtonClick="setOperation" />
    <Button label="4" @onButtonClick="addDigit" />
    <Button label="5" @onButtonClick="addDigit" />
    <Button label="6" @onButtonClick="addDigit" />
    <Button label="-" operation @onButtonClick="setOperation" />
    <Button label="1" @onButtonClick="addDigit" />
    <Button label="2" @onButtonClick="addDigit" />
    <Button label="3" @onButtonClick="addDigit" />
    <Button label="+" operation @onButtonClick="setOperation" />
    <Button label="0" double @onButtonClick="addDigit" />
    <Button label="." @onButtonClick="addDigit" />
    <Button label="=" operation @onButtonClick="setOperation" />
  </div>
</template>

<script>
import Button from "../components/Button";
import Display from "../components/Display";

export default {
  data: function () {
    return {
      displayValue: "0",
      clearDisplay: false,
      operation: null,
      values: [0, 0],
      current: 0,
    };
  },
  components: { Display, Button },
  methods: {
    clearMemory() {
      Object.assign(this.$data, this.$options.data());
    },
    setOperation(operation) {
      if (this.current == 0) {
        this.operation = operation;
        this.current = 1;
        this.clearDisplay = true;
      } else {
        const equals = operation === "=";
        const currentOperation = this.operation;

        try {
          this.values[0] = eval(
            `${this.values[0]}${currentOperation}${this.values[1]}`
          );
        } catch (e) {
          this.$emit("onError", e);
        }

        this.values[1] = 0

        this.displayValue = this.values[0]
        this.operation = equals ? null : operation
        this.current = equals ? 0 : 1
        this.clearDisplay = !equals


      }
    },
    addDigit(digit) {
      console.log('Está chegando até aqui');
      if (digit === "." && this.displayValue.includes(".")) {
        return
      }

      const clearDisplay = this.displayValue === "0" 
        || this.clearDisplay;
      const currentValue = clearDisplay ? "" : this.displayValue;
      const displayValue = currentValue + digit;

      this.displayValue = displayValue;
      this.clearDisplay = false;

      // Opcao 1:
      this.values[this.current] = displayValue;

      // Opcao 2:
      // if (digit != ".") {
      //   const i = this.current;
      //   const newValue = parseFloat(displayValue);
      //   this.values[i] = newValue;
      // }
      // Para executar é: npm run server
    },
  },
};
</script>

<style>
.calculator {
  height: 340px;
  width: 235px;
  border-radius: 5px;
  overflow: hidden;

  display: grid;
  grid-template-columns: repeat(4, 25%);
  grid-template-rows: 1fr 48px 48px 48px 48px 48px;
}
</style>