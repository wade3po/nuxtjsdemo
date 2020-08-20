<template>
  <div class="container">
    <div>
      <Logo/>
      <h1 class="title">nuxtdemo</h1>
      <div class="links">
        <a href="https://www.nuxtjs.cn/" target="_blank" class="button--green">中文文档</a>
        <a href="https://github.com/nuxt/nuxt.js" target="_blank" class="button--grey">GitHub</a>
      </div>
      <p>只是单纯创建一个nuxtjsDemo，然后写几个自己组件的页面凑内容，别怪我一点也不用心，页面只是为了实现功能，很丑</p>
      <nuxt-link to="/WadeUINav" class="button--green" style="margin-top: 20px">wade-ui导航</nuxt-link>
    </div>
  </div>
</template>

<script>
  export default {}
</script>

<style>
  .container {
    margin: 0 auto;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  .title {
    font-family: 'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
    display: block;
    font-weight: 300;
    font-size: 100px;
    color: #35495e;
    letter-spacing: 1px;
  }

  .subtitle {
    font-weight: 300;
    font-size: 42px;
    color: #526488;
    word-spacing: 5px;
    padding-bottom: 15px;
  }

  .links {
    padding-top: 15px;
  }
</style>
