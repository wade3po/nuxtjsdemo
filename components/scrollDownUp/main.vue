<template>
  <div class="" id="scroll"
     @touchstart.stop="touchStart($event)"
     @touchmove="touchMove($event)"
     @touchend="touchEnd($event)">
    <slot></slot>
  </div>
</template>

<script>
  export default {
    props: [ 'refresh', 'load-more', 'bottomDistance', 'move-distanse'],
    data() {
      return {
        startY: 0,
        windowHeight: '',
        downT: '',
        refreshFlag: false
      }
    },
    mounted() {
      if(history.scrollRestoration){
        history.scrollRestoration= 'manual';
      };
      this.windowHeight = document.documentElement.clientHeight || document.body.clientHeight;
      window.addEventListener('scroll', this.onScroll);
    },
    methods: {
      touchStart(e){
        this.startY = e.targetTouches[0].pageY;
      },
      touchMove(e){
        if((document.documentElement.scrollTop || document.body.scrollTop) == 0){
          let moveDistance = e.targetTouches[0].pageY - this.startY;
          if(moveDistance > 0){
            this.refreshFlag = true;
            this.$emit('move-distanse', moveDistance);
          };
        };
      },
      touchEnd(){
        if(this.refreshFlag){
          this.$emit('refresh');
          this.refreshFlag = false;
        };
      },
      onScroll() {
        if(this.downTime){
          clearTimeout(this.downTime);
        };
        this.downTime = setTimeout(() => {
          let contentHeight = document.getElementById('scroll').clientHeight;//容器高度
          let scrollTop = document.documentElement.scrollTop || document.body.scrollTop;//窗口滚动条高度
          if (contentHeight + document.getElementById('scroll').offsetTop - this.windowHeight - scrollTop <= (this.bottomDistance || 0)) {
            //加载更多操作
            this.$emit('load-more');
          }
        }, 200);
      }
    },
    beforeDestroy(){
      window.scrollTo(0, 0);
      window.removeEventListener('scroll', this.onScroll)
    }
  }
</script>
