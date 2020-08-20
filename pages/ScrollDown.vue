<template>
  <div>
    <p v-if="show">加载中。。。</p>
    <w-scroll-down @refresh="refresh" @move-distance="moveDistance">
      <ul>
        <li v-for="val in arrList">{{val}}</li>
      </ul>
    </w-scroll-down>
  </div>
</template>

<script>
  import wScrollDown from '../components/ScrollDown/main'
  export default {
    data(){
      return {
        arrList: [],
        show: false
      }
    },
    components: {wScrollDown},
    created(){
      for (let i = 0; i < 50; i++) {
        this.arrList.push(Math.random())
      }
    },
    methods: {
      refresh(){
        this.show = true;
        setTimeout(() => {
          this.show = false;
          this.arrList = []
          for (let i = 0; i < 50; i++) {
            this.arrList.push(Math.random())
          }
        }, 2000)
      },
      moveDistance(){
        this.show = true;
      }
    }
  }
</script>

<style></style>
