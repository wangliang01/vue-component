<template>
  <el-select v-model="value" v-bind="attrs" @change="handleSelect" filterable :filter-method="filterMethod">
    <el-option v-for="item in computedOptions" :key="item.value" :label="item.label" :value="item.value">
      <!-- <template #label>
        <div v-html="item.label"></div>
      </template> -->
      <div v-html="item.highlight"></div>
    </el-option>
  </el-select>
</template>

<script setup>
import { ref, useAttrs, watchEffect, computed } from 'vue';
import { filterMap } from 'sdm2'
import pinyin from 'js-pinyin';
pinyin.setOptions({ checkPolyphone: true, charCase: 1 });
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



const emit = defineEmits(['update:modelValue'])

const attrs = useAttrs()

const value = ref('')
const query = ref('')

console.log(pinyin.getFullChars('圳'))
const handleSelect = (val) => {
  emit('update:modelValue', val)
}

const filterMethod = (q) => {
  console.log('q', q)
  query.value = q
}

const computedOptions = computed(() => {
  // 使用sdm2的match函数进行模糊匹配
  return filterMap(props.options, query.value, {
    // 忽略大小写匹配
    ignoreCase: true,
    matchStr: (item) => {
      return item.label + pinyin.getFullChars(item.label)
    },
    onMatched: (matchedStr) => {
      return `<span class="highlight">${matchedStr}</span>`
    },
    onMap: ({ str, origin }) => {
      console.log("onMap", str, pinyin.getFullChars(origin.label), origin.label)
      const reg = new RegExp(`${origin.label}<span class="highlight"`)
      return {
        // str 是否匹配origin.label<span class="highlight"
        highlight: (str.startsWith(origin.label)) ? origin.label : str.replace(pinyin.getFullChars(origin.label), ''),
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
:v-deep(.el-select__input) {
  margin-left: 0
}
</style>
