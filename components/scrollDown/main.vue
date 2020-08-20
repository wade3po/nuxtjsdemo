<template>
  <div class="" id="refresh"
       @touchstart="touchStart($event)"
       @touchmove="touchMove($event)"
       @touchend="touchEnd($event)">
    <slot></slot>
  </div>
</template>

<script>
  export default {
    props: ['refresh', 'move-distanse'],
    data() {
        return {
            startY: 0
        }
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
    }
  }
</script>
