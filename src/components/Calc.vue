<template>
  <div>
    <div class="error" v-show="error">{{ error }}</div>-
    <div class="msg">
      <template v-if="result < 0">Отрицательный результат</template>
      <template v-else-if="result > 0">Положительный результат</template>
      <template v-else>Нулевой результат</template>
    </div>
    <div class="main">
      <input type="number" v-model.number="op1">
      <input type="number" v-model.number="op2">
      = {{ result }}<br/>
      fib = {{ fibResult }}
    </div>
    <div class="keyboard">
      <button v-for="operation in operations" :key="operation" @click="calculate(operation)">{{ operation }}</button>
      <div style="padding-top: 30px; padding-bottom: 30px">
        <input type="checkbox" id="checkbox" v-model="kbdChecked">
        <label for="checkbox">Отобразить экранную клавиатуру</label>
        <div class="screenKeyboard" v-show="kbdChecked">
         <div>
            <button v-for="digit in digits" :key="digit" @click="onDigit">{{ digit }}</button>
            <button @click="onBackspace">backspace</button>
          </div>
          <div>
            <input type="radio" id="one" value="1" v-model="picked">
            <label for="one">Операнд 1</label>
            <input type="radio" id="two" value="2" v-model="picked">
            <label for="two">Операнд 2</label>
          </div>
         </div>
      </div>
      <div>
        <button @click="counter++">{{ getCounter }}</button>
      </div>
      <div class="logs">
        {{ logs }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Calc',
  data: () => ({
    op1: 0,
    op2: 0,
    result: 0,
    error: '',
    operations: ['+', '-', '*', '/', '**', '//'],
    logs: {},
    fibResult: 0,
    counter: 0,
    //
    kbdChecked: false,
    digits: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
    picked: '1'
  }),
  methods: {
    onDigit (event) {
      switch (this.picked) {
        case '1': this.op1 = this.addDigit(this.op1, event); break
        case '2': this.op2 = this.addDigit(this.op2, event); break
      }
    },
    addDigit (op, event) {
      if (op === 0) {
        return Number(event.target.innerText)
      } else {
        return op * 10 + Number(event.target.innerText)
      }
    },
    onBackspace () {
      switch (this.picked) {
        case '1': this.op1 = this.delDigit(this.op1); break
        case '2': this.op2 = this.delDigit(this.op2); break
      }
    },
    delDigit (op) {
      if (op === 0) {
        return 0
      } else {
        op = '' + op
        const tmp = op.substring(0, op.length - 1)
        if (tmp.length === 0 || tmp === '-') {
          return 0
        } else {
          return Number(tmp)
        }
      }
    },
    calculate (operation) {
      this.error = ''
      switch (operation) {
        case '+': this.sum(); break
        case '-': this.sub(); break
        case '*': this.mul(); break
        case '/': this.div(); break
        case '**': this.deg(); break
        case '//': this.idiv(); break
      }
      const { op1, op2, result } = this
      this.$set(this.logs, [Date.now()], `${op1} ${operation} ${op2} = ${result}`)
    },
    sum () {
      const { op1, op2 } = this
      this.result = op1 + op2
      this.fibResult = this.fib1 + this.fib2
    },
    sub () {
      const { op1, op2 } = this
      this.result = op1 - op2
    },
    mul () {
      const { op1, op2 } = this
      this.result = op1 * op2
    },
    div () {
      const { op1, op2 } = this
      if (op2 !== 0) {
        this.result = op1 / op2
      } else {
        this.error = 'На 0 делить нельзя!'
      }
    },
    deg () {
      const { op1, op2 } = this
      this.result = Math.pow(op1, op2)
    },
    idiv () {
      const { op1, op2 } = this
      if (op2 !== 0) {
        this.result = Math.floor(op1 / op2)
      } else {
        this.error = 'На 0 делить нельзя!'
      }
    },
    fib (n) {
      if (n === 0 || n === 1) {
        return n
      } else if (n > 1) {
        return this.fib(n - 1) + this.fib(n - 2)
      } else {
        this.error = 'Invalid value'
      }
    }
  },
  computed: {
    // no input parameters! must return value! used cached values!
    getCounter () {
      return `Счетчик нажатий: ${this.counter}`
    },
    fib1 () {
      return this.fib(this.op1)
    },
    fib2 () {
      return this.fib(this.op2)
    }
  }
}
</script>
