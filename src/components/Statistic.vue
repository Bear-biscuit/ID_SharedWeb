<template>
  <el-row class="place-content-center">
    <el-col :span="6" class="el-col">
      <el-statistic title="本页访问人次" :value="pvValue" />
    </el-col>
    <el-col :span="6" class="el-col">
      <el-statistic title="本页访问人数" :value="uvValue" />
    </el-col>
  </el-row>
</template>

<script setup>
import {ref, watch} from 'vue'
import { useTransition } from '@vueuse/core'


// 使用 defineProps 来定义 props
const props = defineProps({
  pv:Number,
  uv:Number
})

// 创建一个 ref 来跟踪 source 值
const sourcepv = ref(props.pv)
const sourceuv = ref(props.uv)

// 使用 useTransition
const pvValue = useTransition(sourcepv, {
  duration: 1500,
})
const uvValue = useTransition(sourceuv, {
  duration: 1500,
})

// 如果父组件传递的值可能会更新，监听 props 的变化
watch(() => props.pv, (newValue) => {
  sourcepv.value = newValue
})
watch(() => props.uv, (newValue) => {
  sourceuv.value = newValue
})
</script>

<style scoped>
.el-col {
  text-align: center;
}
</style>
