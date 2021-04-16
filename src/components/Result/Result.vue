<template>
  <div class="result">
    <h1 class="title">
      Вы откладываете {{result}} ₽ в месяц. <br>
      За три года вы бы заработали:
    </h1>

    <div class="result__container">
      <money :array="mattress" :subtitle="mattressSubtitle" :info="mattressInfo" />
      <money :array="deposit" :subtitle="depositSubtitle" :info="depositInfo" />
      <money :array="invest" :subtitle="investSubtitle" :info="investInfo" />
    </div>

    <div class="result__other-info">

      <div class="result__open" v-if="!show">
        <p class="result__other-text" @click="show = !show">А как в среднем у читателей vc.ru?</p> 
        <svg class="result__other-text" width="16" height="7" viewBox="0 0 16 7" fill="none" xmlns="http://www.w3.org/2000/svg" @click="show = !show">
          <path d="M1 1L7.55598 5.95238L14.0892 1" stroke="#FE4D4A" stroke-width="2" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </div>

      <div class="result__close" v-if="show">
        <div class="close__reader-info" v-if="average<=10000">
          <img class="close__coins_10" src="../../images/coins.png" />
          <p class="close__close-value">~{{average}} ₽</p>
        </div>
        <div class="close__reader-info" v-else-if="10000<average && average<=20000">
          <img  class="close__bills_20" src="../../images/bills.png" />
          <img class="close__coins_20" src="../../images/coins.png" />
          <p class="close__close-value">~{{average}} ₽</p>
        </div>
        <div class="close__reader-info" v-else-if="20000<average && average<=30000">
          <img  class="close__bills_30" src="../../images/bills_2.png" />
          <img class="close__coins_30" src="../../images/coins.png" />
          <p class="close__close-value">~{{average}} ₽</p>
        </div>
        <div class="close__reader-info" v-else-if="30000<average && average<=40000">
          <img  class="close__bills_40" src="../../images/bills_2.png" />
          <img class="close__coins_40" src="../../images/coins_4.png" />
          <p class="close__close-value">~{{average}} ₽</p>
        </div>
        <div class="close__reader-info" v-else-if="40000<average && average<=50000">
          
          
          <img  class="close__bills_53" src="../../images/bills_4.png" />
          <img  class="close__bills_52" src="../../images/bills_3.png" />
          <img  class="close__bills_51" src="../../images/bills_2.png" />
          <img class="close__coins_52" src="../../images/coins_3.png" />
          <img class="close__coins_51" src="../../images/coins_2.png" />
          
          <p class="close__close-value">~{{average}} ₽</p>
        </div>
        <p class="close__text">в среднем откладывают читатели vc.ru</p>
        <div class="close__diagrams">
          <div class="diagrama">
            <svg
              width="180"
              height="180"
              viewBox="0 0 120 120"
            >
              <circle
                cx="60"
                cy="60"
                r="36"
                fill="none"
                stroke="#FFFFFF"
                stroke-width="9"
                stroke-dashoffset="0"
                stroke-dasharray="0"
              />
              <circle
                cx="60"
                cy="60"
                r="41"
                fill="none"
                :stroke-dashoffset=diagramma1000
                stroke-dasharray="257.48"
                stroke="#FE4D4A"
                stroke-width="20"
                transform="rotate(-90 60 60)"
              />
            </svg>
            <p class="diagrama__procent">{{procent1000}}%</p>
            <p class="diagrama__text">читателей откладывают больше 1000 ₽ в месяц</p>
          </div>
          <div class="diagrama">
            <svg
              width="180"
              height="180"
              viewBox="0 0 120 120"
            >
              <circle
                cx="60"
                cy="60"
                r="36"
                fill="none"
                stroke="#FFFFFF"
                stroke-width="9"
                stroke-dashoffset="0"
                stroke-dasharray="0"
              />
              <circle
                cx="60"
                cy="60"
                r="41"
                fill="none"
                :stroke-dashoffset=diagramma10000
                stroke-dasharray="257.48"
                stroke="#FE4D4A"
                stroke-width="20"
                transform="rotate(-90 60 60)"
              />
            </svg>
            <p class="diagrama__procent">{{procent10000}}%</p>
            <p class="diagrama__text">читателей откладывают больше 10000 ₽ в месяц</p>
          </div>

        </div>
        <div class="result__open">
          <p class="result__other-text" @click="show = !show">Свернуть</p>
          <svg class="result__other-text" width="16" height="7" viewBox="0 0 16 7" fill="none" xmlns="http://www.w3.org/2000/svg" @click="show = !show">
          <path d="M14.0891 5.95242L7.53313 1.00004L0.999928 5.95242" stroke="#FE4D4A" stroke-width="2" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </div>
      </div>
    </div>
    <div class="footer">
      <p class="footer__text">Как начать инвестировать?</p>
      
      <a href="https://alfabank.ru/make-money/investments/" target="_blank">
        <button class="footer__button">Узнать</button>
      </a>
    </div>
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
      diagramma1000:function(){
        return (257.48-this.procent1000*2.5748)
      },
      diagramma10000:function(){
        return (257.48-this.procent10000*2.5748)
      }
    },
    data() {
      return{
        show: false,
        average:49000,
        procent1000: 70,
        procent10000: 7,
        mattressSubtitle: "если откладывать под матрас",
        mattressInfo: "В этом мало смысла — такие накопления «съедает» инфляция",
        depositSubtitle: "если откладывать на депозит",
        depositInfo: "Ставки по вкладам различны в разных банках и зависят от многих факторов, в частности, от ключевой ставки Центрального банка РФ¹.",
        investSubtitle: "если инвестировать в ПИФ «Альфа-Капитала»",
        investInfo: "Вы становитесь инвестором набора компаний, который определяют профессиональные управляющие. Они решают, когда покупать и продавать ценные бумаги, чтобы обеспечить инвестиционный доход. Купить или продать паи фонда можно в любой момент².",
      }
    },
    components:{
        Money
    }
  }
</script>

<style scoped>
  @import '../../style/index.css';
</style>
