<template>
  <div class="result">
    <h1 class="title">
      Вы откладываете {{result}} ₽ в месяц. <br>
      За три года вы бы заработали:
    </h1>
    <!-- <h3>{{mattress}}</h3>
    <div class="money__container">
      <template v-for="n in first" v-bind:key="n">
        <img class="money__image"  src="../../images/Money.png" :style="{'left':array}" />
      </template>
    </div> -->
    <div class="result__container">
      <money :array="mattress" :subtitle="mattressSubtitle" :info="mattressInfo" />
      <money :array="deposit" :subtitle="depositSubtitle" :info="depositInfo" />
      <money :array="invest" :subtitle="investSubtitle" :info="investInfo" />
    </div>
    <!-- <h3>{{deposit}}</h3>
    <h3>{{invest}}</h3> -->

  </div>
</template>

<script>
import Money from '../Money/Money.vue'
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
      // number: 3,
    },
    computed: {
      mattress : function(){
        return [this.result*12*3, Math.floor(this.result*12*3/this.oneCoin)]
      },
      deposit: function(){
        let sum = this.result*12
        for (let i=0; i<3; i++){
          sum = this.result*12*(i+1) + sum*0.0698
        }
        return [Math.floor(sum), Math.floor(sum/this.oneCoin)]
      }, 
      invest: function(){
        return [Math.floor(this.result*12*3 + this.result*12*3*0.7121), 10]
      },
      oneCoin:function(){
        return Math.floor(this.invest[0]/10)
      },
      // array: function(){
      //   let x=400+6
      //   return `${x}px`
      // },

    },
    data() {
      return{

        mattressSubtitle: "если откладывать под матрас",
        mattressInfo: "В этом мало смысла — такие накопления «съедает» инфляция",
        depositSubtitle: "если откладывать на депозит",
        depositInfo: "Ставки по вкладам различны в разных банках и зависят от многих факторов, в частности, от ключевой ставки Центрального банка РФ¹.",
        investSubtitle: "если инвестировать в ПИФ «Альфа-Капитала»",
        investInfo: "Вы становитесь инвестором набора компаний, который определяют профессиональные управляющие. Они решают, когда покупать и продавать ценные бумаги, чтобы обеспечить инвестиционный доход. Купить или продать паи фонда можно в любой момент².",
        // year : 12,
        // mattress = year*3,
        // deposit = (year+year*0.698)+year+((year+year*0.698)+year)*0.698+year+(((year+year*0.698)+year)*0.698+year)*0.698,
      }
    },
    methods: {
      // year = result*12,
      // mattress = year*3,
    },
    components:{
        Money
      // 'money': {
      //   // 'props':['users'],
      //   render:function () {
      //     for(let i=0; i<4; i++) {
      //       return <img  src="../../images/Money.png" />
      //     } 
      //   }
      // }
    }
  }
</script>

<style scoped>
  /* .money__image {
    --left: {{ year }};
  } */
  @import '../../style/index.css';
</style>
