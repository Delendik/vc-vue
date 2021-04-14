<template>
  <div class="range">
    <h1 class="title">Сколько денег вы откладываете в месяц?</h1>
    <p class="text">Ответьте и узнаете, сколько копят другие.</p>
    <div class="range__container">
      <p class="range__container-text">0	&#8381;</p>
      <input 
        type="range" 
        class="range__line" 
        min= 0
        max= 50000 
        step=1
        v-model.number="currentValue"
        @change="viewResult"
      >
      <output class="range__value" v-html=currentValue></output>
      <p class="range__container-text">50000	&#8381;</p>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Range',
    // render: {
    //   document.getElementsByClassName('range__value')[0].style= "margin: 50px";
    // }
    watch: {
      'currentValue': function (v) {
        if (v) {
          let num = 35+454/50000*this.currentValue*0.9
          document.getElementsByClassName('range__value')[0].style= `left:${num}px`;
        }
      },
    },
    props: {
      from: Number,
      to: Number
    },
    data() {
      return{
        currentValue: 0,
        val: "",
        showResult: false,
        result: 0,
      }
    },
    methods: {
      onChange() {
          if(1000<this.currentValue<10000){
            this.val = Math.floor(this.currentValue/1000)+" "+this.currentValue%1000+ ` &#8381;`;
          }
      },
      viewResult(){
          if(this.currentValue>0){
            this.showResult = true;
            this.result = this.currentValue;
            this.$emit("viewResult", [this.showResult, this.result])
          }
      }
    }
  }
</script>

<style scoped>
  @import '../../style/index.css';
</style>
