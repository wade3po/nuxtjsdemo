<template>
  <ul class="nav-list">
    <li @click="toast">Toast</li>
    <li><nuxt-link to="/Swiper">Swiper</nuxt-link></li>
    <li><nuxt-link to="/ScrollDown">ScrollDown下拉刷新</nuxt-link></li>
    <li><nuxt-link to="/ScrollUp">ScrollUp上拉加载</nuxt-link></li>
    <li><nuxt-link to="/ScrollDownUp">ScrollDownUp上拉加载下拉刷新</nuxt-link></li>
    <li><nuxt-link to="/MoveJudge">MoveJudge左滑右滑</nuxt-link></li>
    <li><nuxt-link to="/Picker">Picker不联动</nuxt-link></li>
    <li><nuxt-link to="/PickerLink">PickerLink联动</nuxt-link></li>
    <li><nuxt-link to="/DisableScroll">DisableScroll遮罩下禁止滚动</nuxt-link></li>
  </ul>
</template>
<script>
  import Toast from '../components/Toast'
  export default {
    methods: {
      toast(){
        Toast('自定义toast组件弹窗', 3000);
      }
    }
  }
</script>
<style>
  li{
    list-style: none;
  }
  .nav-list{
    margin: 30px 0 0 30px;
    cursor: pointer;
  }
  .nav-list li{
    margin-top: 10px;
  }
</style>
