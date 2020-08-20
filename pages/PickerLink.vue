<template>
  <div>
    <p @click="show = true">显示</p>
    <p>选中：{{val}}</p>
    <div v-if="show">
      <w-picker-link
        :data="list"
        @confirm="confirm"
        @cancel="cancel"
        title="标题"
        column="3"
        :defaultValue="defaultValue">
      </w-picker-link>
    </div>
  </div>
</template>

<script>
  import wPickerLink from '../components/pickerLink/main'
  import area from '../components/pickerLink/area'
  export default {
    data(){
      return {
        defaultValue: ['福建', '厦门市', '湖里区'],
        list: [
          {
            value: '福建省',
            data: [
              {value: '福州市', data: [{value: '台江区'},{value: '鼓楼区'}]},
              {value: '厦门市', data: [{value: '思明区'},{value: '湖里区'}]}
            ]
          },
          {
            value: '浙江省',
            data: [
              {value: '杭州市', data: [{value: '上城区'},{value: '下城区'}]}
            ]
          }
        ],
        show: true,
        val: ''
      }
    },
    components: {wPickerLink},
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

<style></style>
