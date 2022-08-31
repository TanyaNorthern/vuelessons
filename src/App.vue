<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
<!--    <button v-on:click="counter++">{{ counter }}</button>-->
<!--    <button @click="counter++">{{ counter }}</button>-->
<!--    <button @click="increase(2, $event)">{{ counter }}</button>-->
<!--    <button @click="reset">Reset</button>-->
<!--    <input-->
<!--      type="text"-->
<!--      placeholder="text"-->
<!--      @blur="blur"-->
<!--      @focus="focus"-->
<!--      @change="change"-->
<!--      @input="input"-->
<!--      v-model.lazy="txt"-->
<!--    >-->
<!--    <p>{{ txt }}</p>-->
    <Calc/>
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
    txt: ''
  }),
  methods: {
    increase (step, event) {
      console.log(event)
      this.counter += step
    },
    reset () {
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
