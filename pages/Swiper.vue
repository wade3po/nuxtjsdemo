<template>
  <div style="height: 200px">
    <Swiper :wSwiperOptions="wOptions">
      <div id="wSwiperWrap">
        <div class="w-slide" style="background: #ffa142">11111111</div>
        <div class="w-slide" style="background: #31d2fa">22222222222</div>
        <div class="w-slide" style="background: yellow">333333333333</div>
        <div class="w-slide" style="background: saddlebrown">444444444</div>
      </div>
      <div class="w-prev-slide-btn"><</div>
      <div class="w-next-slide-btn">></div>
    </Swiper>
  </div>
</template>

<script>
  import Swiper from '../components/swiper/main'
  export default {
    data(){
      return {
        wOptions: {
          pageShow: true,
          speed: .1,
          time: 2000,
          autoPlay: true,
          hoverPause: true
        }
      }
    },
    components: {Swiper}
  }
</script>

<style></style>
