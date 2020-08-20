<template>
  <div>
    <p @click="show = true">显示</p>
    <p>选中：{{val}}</p>
    <div v-if="show">
      <w-picker :dataList="list" @confirm="confirm"
                @cancel="cancel" title="标题"></w-picker>
    </div>
  </div>
</template>

<script>
  import wPicker from '../components/picker/main'
  export default {
    data(){
      return {
        list:[[{value: '福建省'}, {value: '浙江省'}],[{value: '厦门市'},{value: '杭州市'}]],
        show: true,
        val: ''
      }
    },
    components: {wPicker},
    methods: {
      cancel(){
        this.show = false;
      },
      confirm(val){
        this.val = val;
        this.show = false;
      },
    }
  }
</script>

<style scoped>
  *{
    margin: 0;
    padding: 0;
  }
</style>
