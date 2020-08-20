<template>
  <div>
    <move-judge @moveJudge="moveJudge"
                @moveDistance="moveDistance"
                margin="50">
      <div style="width: 100%;overflow: hidden;height: 1000px;background: rgba(71,73,78,0.22)">
        <p style="text-align: center;font-size: 20px;margin-top: 30px">{{judge}}</p>
      </div>
    </move-judge>
  </div>
</template>

<script>
  import moveJudge from '../components/moveJudge/main'
  export default {
    data(){
      return {
        judge: ''
      }
    },
    components: {moveJudge},
    methods: {
      moveJudge(val){
        this.judge = val + '滑动了'
      },
      moveDistance(){

      }
    }
  }
</script>

<style></style>
