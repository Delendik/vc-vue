<template>
  <div class="result">
    <h1 class="title">
      Вы откладываете {{result}} ₽ в месяц. <br>
      За три года вы бы заработали:
    </h1>
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
    data() {
      return{
      }
    },
    methods: {
    }
  }
</script>

<style scoped>
  @import '../../style/index.css';
</style>
