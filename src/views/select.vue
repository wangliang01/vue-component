<template>
  <div>
    <VSelect :options="options" v-model="value"></VSelect>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import VSelect from '../components/Select.vue'

const value = ref('Beijing');

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

<style lang="scss" scoped></style>
