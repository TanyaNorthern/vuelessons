<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <Calc v-if="show"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Calc from '@/components/Calc.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Calc
  },
  data: () => ({
    counter: 0,
    show: true,
    collection: [1, 2, 3, 4, 5, 6, 7],
    arr: [
      {
        text: 'qwe',
        show: true
      },
      {
        text: 'rty',
        show: true
      },
      {
        text: 'uio',
        show: false
      }
    ]
  }),
  methods: {
    increase (step, event) {
      console.log(event)
      this.counter += step
    },
    reset (event) {
      console.log(event)
      this.counter = 0
    },
    blur () {
      console.log('blur')
    },
    focus () {
      console.log('focus')
    },
    change () {
      console.log('change')
    },
    input () {
      console.log('input')
    }

  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
