<template>
  <div>
    <p v-if="show">加载中。。。</p>
    <w-scroll
      @refresh="refresh"
      @load-more="loadMore"
      @move-distance="moveDistance"
      bottomDistance="20">
      <div>
        <ul>
          <li v-for="val in arrList">{{val}}</li>
        </ul>
      </div>
    </w-scroll>
    <p v-if="show">加载中。。。</p>
  </div>
</template>

<script>
  import wScroll from '../components/scrollDownUp/main'
  export default {
    data(){
      return {
        arrList: [],
        show: false
      }
    },
    components: {wScroll},
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
      },
      loadMore(){
        this.show = true;
        setTimeout(() => {
          this.show = false;
          for (let i = 0; i < 50; i++) {
            this.arrList.push(Math.random())
          }
        }, 2000)
      }
    }
  }
</script>

<style></style>
