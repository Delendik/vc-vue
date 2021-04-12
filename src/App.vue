<template>
  <Range @viewResult="viewResult" />
  <Result :result="result" :showResult="showResult" />
</template>

<script>
  import Range from './components/Range/Range.vue'
  import Result from './components/Result/Result.vue'

  export default {
    name: 'App',
    components: {
      Range,
      Result
    },
    data() {
      return{
        result: 0,
        showResult: false,
      }
    },
    methods: {
      viewResult(data){
        this.showResult = data[0];
        this.result = data[1];
      }
    }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
  #app{
    width: 640px;
    margin: 0 auto;
  }
</style>
