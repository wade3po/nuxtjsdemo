<template>
  <div>
    <w-scroll-up @load-more="loadMore" :bottom-distance="10">
      <ul>
        <li v-for="val in arrList">{{val}}</li>
      </ul>
    </w-scroll-up>
    <p v-if="show">加载中。。。</p>
  </div>
</template>

<script>
  import wScrollUp from '../components/scrollUp/main'
  export default {
    data(){
      return {
        arrList: [],
        show: false
      }
    },
    components: {wScrollUp},
    created(){
      for (let i = 0; i < 50; i++) {
        this.arrList.push(Math.random())
      }
    },
    methods: {
      loadMore(){
        this.show = true;
        setTimeout(() => {
          this.show = false;
          for (let i = 0; i < 50; i++) {
            this.arrList.push(Math.random())
          }
        }, 2000)
      },
    }
  }
</script>

<style></style>
