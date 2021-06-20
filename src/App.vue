<template>
  <calculator></calculator>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');
body{
  font-family: "Montserrat", sans-serif;
  background-color: #a5a5a5;
}
</style>
