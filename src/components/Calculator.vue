<template>
  <div class="container">
    <!-- Calculator application -->
    <div class="calc p-3 rounded" style="max-width: 400px; margin: 50px auto; background: #1768AC">
      <!-- Result -->
      <div class="w-full rounded m-1 p-3 lead text-white bg-blue" style="text-align: right; font-weight: bold;">
        {{state.val || 0}}
      </div>
      <!-- Button -->
      <div class="row no-gutters">
        <div class="col-3" v-for="n in state.elements" :key="n">
          <div class="lead text-white text-center m-1 p-3 bg-blue rounded hover-class"
          style="font-weight: bold"
          @click="action(n)"
          >
          {{n}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from 'vue';

export default {
  name: 'Calculator',
  setup() {
    const state = reactive({
      val: '',
      elements: ['C', '%', '/', '*', 7, 8, 9, '-', 4, 5, 6, '+', 1, 2, 3, '=', 0, '.' ],
      operator: null,
      preVal: ''
    })

    function action(n) {
      const hasAppendValue = !isNaN(n) || n === '.';
      const hasClear = n === 'C';
      const hasPercents = n === '%';
      const hasOperator = ['/','*','-','+'].includes(n);
      const hasEqual = n === '=';

      if(hasAppendValue){
      state.val += n + '';
      }
      if(hasClear){
        state.val = '';
      }
      if(hasPercents){
        state.val = state.val / 100 + '';
      }
      if(hasOperator){
        state.operator = n;
        state.preVal = state.val;
        state.val = '';
      }
      if(hasEqual){
        state.val = eval(
          state.preVal + state.operator + state.val
        );
        state.preVal = '';
        state.operator = null;
      }
    }

    return {
      state,
      action
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bg-blue{
  background: #2541B2;
}
.hover-class:hover{
  cursor: pointer;
  background: #06BEE1;
  transition: 0.5s;
}
.calc{
  box-shadow: 0 10px 20px rgba(0,0,0,0.40), 0 6px 6px rgba(0,0,0,0.63);
}
</style>
