<template>
  <view class="cu-item" >
    <view class="content flex">
      <view class="text-black">{{title}}</view>
      <view v-if="need" class="text-red" >*</view>
    </view>
    <view class="action">
      <input  v-if="editable" class="text-right" :type="isNick ? 'nickname': '' " :placeholder="placeholder"  @input="onInput" v-model="modelvalue"/>
      <text v-else class="text-grey">{{modelvalue}}</text>
      </view>
  </view>
</template>
<script>
export default {
  name: 'color-input',
  emits:['change'],
  props: {
    need:{
      type: Boolean,
      default: false
    },
    title: {
      type: String,
      default: ""
    },
    placeholder:{
      type: String,
      default: ""
    },
    value:{
      type: String,
      default: ""
    },
    isNick:{
      type: Boolean,
      default: false
    },
    editable:{
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      modelvalue:""
    }
  },
  watch: {
    value(newVal){
      console.log('color-input watch value1:',newVal)
      this.modelvalue = newVal;
      console.log('color-input watch value2:',this.modelvalue)
    },  
  },
  methods: {
    onInput() {
      this.changeData();
		},
    changeData() {
      this.$emit('change',this.modelvalue)
      // console.log('color-input changeData:',this.modelvalue)
    },
  },
  created(){
    // console.log('color-input created 1:',{value:this.value})
    this.modelvalue = this.value
    console.log('color-input require 2:',this.require)
  },
  options: {
    // 微信小程序中 options 选项
    virtualHost: true, //  将自定义节点设置成虚拟的，更加接近Vue组件的表现。我们不希望自定义组件的这个节点本身可以设置样式、响应 flex 布局等，而是希望自定义组件内部的第一层节点能够响应 flex 布局或者样式由自定义组件本身完全决定
  },
}
</script>
