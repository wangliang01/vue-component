<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)

const value = ref('')

const options = [
  {
    label: '选项1',
    value: 'shanghai',
  },
  {
    label: '选项2',
    value: 'beijing',
  },
]
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <el-pro-select v-model="value" :options="options"></el-pro-select>
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
