<template>
  <div class="container">
    <!-- Calculator application -->
    <div class="calc p-3 rounded" style="max-width: 400px; margin: 50px auto; background: #fff">
      <!-- Result -->
      <div class="w-full rounded m-1 p-3 lead text-black bg-blue" style="text-align: right; font-weight: bold;">
        {{val || 0}}
      </div>
      <!-- Button -->
      <div class="row no-gutters">
        <div class="col-3" v-for="n in elements" :key="n">
          <div class="lead text-black text-center m-1 p-3 bg-blue rounded hover-class"
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
export default {
  name: 'Calculator',
  props: {
    msg: String
  },
  data() {
    return {
      val: '',
      elements: ['C', '%', '/', '*', 7, 8, 9, '-', 4, 5, 6, '+', 1, 2, 3, '=', 0, '.' ],
      operator: null,
      preVal: '',
    }
  },

  methods: {
    action(n){

      if(!isNaN(n) || n === '.'){
      this.val += n + '';
      }

      if(n === 'C'){
        this.val = '';
      }

      if(n === '%'){
        this.val = this.val / 100 + '';
      }

      if(['/','*','-','+'].includes(n)){
        this.operator = n;
        this.preVal = this.val;
        this.val = '';
      }

      if(n === '='){
        this.val = eval(
          this.preVal + this.operator + this.val
        );
        this.preVal = '';
        this.operator = null;
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bg-blue{
  background: #B2F7EF;
}

.hover-class:hover{
  cursor: pointer;
  background: #a5a5a5;
  transition: 0.5s;
}
.calc{
  box-shadow: 0 10px 20px rgba(0,0,0,0.40), 0 6px 6px rgba(0,0,0,0.63);
}
</style>
