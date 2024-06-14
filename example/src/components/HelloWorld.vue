<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)

const value = ref('')

const options = [
{
    value: 'Beijing',
    label: '北京',
  },
  {
    value: 'Shanghai',
    label: '上海',
  },
  {
    value: 'Nanjing',
    label: '南京',
  },
  {
    value: 'Chengdu',
    label: '成都',
  },
  {
    value: 'Shenzhen',
    label: '深圳',
  },
  {
    value: 'Guangzhou',
    label: '广州',
  },
]
</script>

<template>
  <el-pro-select v-model="value" :options="options"></el-pro-select>
 
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
