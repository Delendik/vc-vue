<template>
  <div class="money">
    <div class="no-display">{{test}}</div>
    <div class="money__container">
      <template v-for="n in array[1]" v-bind:key="n">
        <img class="money__image"  src="../../images/Money.png" :style="{'left':margin[n-1]}" />
      </template>
    </div>
    <h3 class="money__title">~{{array[0].toLocaleString('ru')}} ₽</h3>
    <p class="money__subtitle">{{subtitle}}  <img src="../../images/info.png" @mouseenter="show = !show" @mouseleave="show = !show" /></p>
    <p class="money__info" v-if="show">{{info}}</p>
  </div>
</template>

<script>
  export default {
    name: 'Money',
    props: {
      array: Array,
      subtitle: String,
      info: String,
    },
    computed: {
      mattress : function(){
        return [this.result*12*3, Math.floor(this.result*12*3/this.oneCoin)]
      },
      test : function(){
        let newArray = []
        for(let i=0; i<this.array[1]; i++){
          newArray.push(i*15)
        }
        newArray.forEach(item=>this.margin.push(`${item}px`))
        return newArray
      }
    },
    data() {
      return{
        margin: [],
        show: false
      }
    },
  }
</script>

<style scoped>
  @import '../../style/index.css';
</style>
