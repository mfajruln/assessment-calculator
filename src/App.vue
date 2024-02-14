<template>
  <div class="calculator" @keydown="handleKeyDown">
    <input type="text" v-model="expression" class="result-display" disabled>
    <div class="buttons">
      <button v-for="button in buttons" :key="button" @click="appendToExpression(button)">{{ button }}</button>
      <button @click="calculate" class="equal-btn">=</button>
      <button @click="clear" class="clear-btn">C</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      expression: '',
      buttons: ['1', '2', '3', '+', '4', '5', '6', '-', '7', '8', '9', '*', '0', '.', '/']
    };
  },
  methods: {
    appendToExpression(char) {
      this.expression += char;
    },
    clear() {
      this.expression = '';
    },
    calculate() {
      try {
        this.expression = eval(this.expression).toString();
      } catch (error) {
        alert('Invalid expression');
        this.expression = '';
      }
    },
    handleKeyDown(event) {
      const key = event.key;
      if (this.buttons.includes(key)) {
        this.appendToExpression(key);
      } else if (key === 'Enter') {
        this.calculate();
      } else if (key === 'Backspace') {
        this.expression = this.expression.slice(0, -1);
      } else if (key === 'Escape') {
        this.clear();
      }
    }
  }
};
</script>

<style>
.calculator {
  width: 280px;
  margin: auto;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.result-display {
  width: 100%;
  margin-bottom: 10px;
  padding: 10px;
  font-size: 24px; /* Increase font size for better visibility */
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

button {
  width: 50px;
  height: 50px;
  border: none;
  background-color: #f2f2f2;
  color: #333;
  font-size: 20px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #e0e0e0;
}

.equal-btn, .clear-btn {
  grid-column: span 2;
}

.clear-btn {
  background-color: #ff6666;
  color: #fff;
}
</style>
