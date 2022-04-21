<template>
  <h1></h1>
  <div class="output">
    <div>{{ string }}</div>
    <div class="outputCalc">{{ calculatorValue || 0 }}</div>
  </div>
  <div class="buttons">
    <div
      class="button"
      v-for="n in btnArr"
      :key="n"
      :class="{ operator: ['C', '*', '/', '-', '+', '%', '='].includes(n) }"
    >
      <div class="btn" @click="action(n)">
        {{ n }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      string: '',
      calculatorValue: '',
      btnArr: ['C', '*', '/', '-', '7', '8', '9', '+', '4', '5', '6', '%', '1', '2', '3', '=', '0', '.'],
      operator: null,
      previousCalculatorValue: '',
    };
  },
  methods: {
    action(n) {
      //Append value to string
      if (!isNaN(n) || n === '.') {
        this.string = `${this.string}${n}`;
        this.calculatorValue += n + '';
      }

      //User clear Calculator
      if (n === 'C') {
        this.string = '';
        this.calculatorValue = '';
      }

      //User press % button
      if (n === '%') {
        this.calculatorValue = this.calculatorValue / 100 + '';
      }
      if (['/', '*', '-', '+'].includes(n)) {
        this.operator = n;
        this.string = `${this.string}${n}`;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = '';
      }
      if (n === '=') {
        this.calculatorValue = eval(this.previousCalculatorValue + this.operator + this.calculatorValue);
        this.previousCalculatorValue = '';
        this.operator = null;
      }
    },
  },
};
</script>

<style>
h1 {
  margin-top: 100px;
  text-align: center;
}
.output {
  text-align: right;
  background-color: antiquewhite;
  width: min(300px, 70%);
  margin: 10px auto;
  padding: 10px;
  border: 0.5px solid rgb(255, 198, 124);
  border-radius: 4px;
  box-shadow: 2.8px 2.8px 2.2px rgba(0, 0, 0, 0.008), 6.7px 6.7px 5.3px rgba(0, 0, 0, 0.012),
    12.5px 12.5px 10px rgba(0, 0, 0, 0.015), 22.3px 22.3px 17.9px rgba(0, 0, 0, 0.018),
    41.8px 41.8px 33.4px rgba(0, 0, 0, 0.022), 100px 100px 80px rgba(0, 0, 0, 0.03);
}
.outputCalc {
  background-color: rgb(255, 209, 148);
  padding: 15px;
  border-radius: 3px;
}
.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: min(300px, 70%);
  border: 0.2px solid rgb(255, 198, 124);
  border-radius: 4px;
  align-items: center;
  background-color: antiquewhite;
  justify-content: center;
  margin: 10px auto;
  gap: 5px;
  box-shadow: 2.8px 2.8px 2.2px rgba(0, 0, 0, 0.008), 6.7px 6.7px 5.3px rgba(0, 0, 0, 0.012),
    12.5px 12.5px 10px rgba(0, 0, 0, 0.015), 22.3px 22.3px 17.9px rgba(0, 0, 0, 0.018),
    41.8px 41.8px 33.4px rgba(0, 0, 0, 0.022), 100px 100px 80px rgba(0, 0, 0, 0.03);
}
.button {
  background-color: rgb(255, 209, 148);
  padding: 6px;
  border-radius: 3px;
  margin: 4px;
  font-size: 1.5em;
  font-weight: bold;
  color: #000;
  text-align: center;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}
.button:hover {
  background-color: rgb(238, 167, 75);
  color: #000;
}
.operator {
  background-color: rgb(238, 167, 75);
  color: #000;
}
.operator:hover {
  background-color: rgb(255, 209, 148);
}
.MyId:hover {
  cursor: pointer;
  filter: brightness(130%);
}
footer {
  text-align: center;
  width: min(300px, 90%);
  border-radius: 3px;
  margin: 100px auto;
  background-color: #0000002a;
  padding: 10px;
  font-weight: bold;
  color: #444;
  text-transform: capitalize;
  box-shadow: 2.8px 2.8px 2.2px rgba(0, 0, 0, 0.008), 6.7px 6.7px 5.3px rgba(0, 0, 0, 0.012),
    12.5px 12.5px 10px rgba(0, 0, 0, 0.015), 22.3px 22.3px 17.9px rgba(0, 0, 0, 0.018),
    41.8px 41.8px 33.4px rgba(0, 0, 0, 0.022), 100px 100px 80px rgba(0, 0, 0, 0.03);
}
</style>
