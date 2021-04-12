<template>
  <div class="result">
    <h1 class="title">
      Вы откладываете {{result}} ₽ в месяц. <br>
      За три года вы бы заработали:
    </h1>
    <h3>{{mattress}}</h3>
    <h3>{{deposit}}</h3>
    <p class="text">Ответьте и узнаете, сколько копят другие.</p>

  </div>
</template>

<script>
  export default {
    name: 'Result',
    watch: {
      'showResult': function (v) {
        if (v) {
          if(this.showResult){
            document.querySelector(".result").classList.add("result_visible")
          }
        }
      },
    },
    props: {
      result: Number,
      showResult: Boolean,
    },
    computed: {
      mattress : function(){
        return this.result*12*3
      },
      deposit: function(){
        let sum = 8888*12

        for (let i=0; i<3; i++){
          
          sum = sum*(i+1) + sum*0.0698
          
          console.log(Math.floor(sum))
        }
        // const year = this.result*12
        return Math.floor(sum)
        // Math.floor((year+year*0.0698)+year+((year+year*0.0698)+year)*0.0698+year+(((year+year*0.698)+year)*0.0698+year)*0.0698)
      }
    },
    data() {
      return{
        // year : result*12,
        // mattress = year*3,
        // deposit = (year+year*0.698)+year+((year+year*0.698)+year)*0.698+year+(((year+year*0.698)+year)*0.698+year)*0.698,
      }
    },
    methods: {
      // year = result*12,
      // mattress = year*3,
    }
  }
</script>

<style scoped>
  @import '../../style/index.css';
</style>
