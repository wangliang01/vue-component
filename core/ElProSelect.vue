<template>
  <el-select v-model="value" v-bind="attrs" @change="handleSelect" filterable :filter-method="filterMethod">
    <el-option v-for="item in computedOptions" :key="item.value" :label="item.label" :value="item.value">
      <div v-html="item.highlight"></div>
    </el-option>
  </el-select>
</template>

<script setup>
import { ref, useAttrs, watchEffect, computed } from 'vue';
import { filterMap } from 'sdm2'
import pinyin from 'pinyin'
import { ElSelect, ElOption } from 'element-plus'
import 'element-plus/theme-chalk/index.css'
import './style.css'

const props = defineProps({
  modelValue: {
    type: String,
    default: ''
  },
  options: {
    type: Array,
    default: () => []
  }
})

function toPinyinString(text, style = pinyin.STYLE_NORMAL) {
  return pinyin(text, {
    style,
    heteronym: true,              // 启用多音字模式
    segment: true,
  }).reduce((acc, cur) => {
    return acc + cur[0]
  }, '')
}


const emit = defineEmits(['update:modelValue'])

const attrs = useAttrs()

const value = ref('')
const query = ref('')

const handleSelect = (val) => {
  emit('update:modelValue', val)
}

const filterMethod = (q) => {
  query.value = q
}

const computedOptions = computed(() => {
  // 使用sdm2的match函数进行模糊匹配
  return filterMap(props.options, query.value, {
    // 忽略大小写匹配
    ignoreCase: true,
    matchStr: (item) => {
      return item.label + toPinyinString(item.label)
    },
    onMatched: (matchedStr) => {
      return `<span class="highlight">${matchedStr}</span>`
    },
    onMap: ({ str, origin }) => {
      const reg = new RegExp(`${origin.label}<span class="highlight"`)
      return {
        highlight: (str.startsWith(origin.label)) ? origin.label : str.replace(toPinyinString(origin.label), ''),
        ...origin,
      }
    }
  })
})

watchEffect(() => {
  value.value = props.modelValue
})
</script>

<style lang="scss" scoped>

</style>
