<template>
  <div>
    <p style="text-align: center;position: fixed;top: 0" @click="hidden('true')">显示遮罩</p>
    <ul>
      <li v-for="val in arrList">{{val}}</li>
    </ul>
    <div class="fixed-wrap" v-show="show" @click="hidden('false')">

    </div>
  </div>
</template>

<script>
  import {disableScroll} from '../components/function'
  export default {
    data(){
      return {
        arrList: [],
        show: true
      }
    },
    created(){
      for (let i = 0; i < 50; i++) {
        this.arrList.push(i)
      }
      disableScroll(true)
    },
    methods: {
      hidden(bool){
        bool = bool === 'false' ? false : true;
        this.show = bool;
        disableScroll(bool)
      }
    }
  }
</script>

<style scoped>
  .fixed-wrap{
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, .2);
  }
</style>
