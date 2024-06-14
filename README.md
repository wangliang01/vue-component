## 功能概述
该组件是对Element Plus的<el-select>组件的封装，增强了筛选功能，实现了拼音辅助的模糊搜索匹配。

**特性**
* 模糊搜索：通过filterable属性启用el-select的筛选功能，并自定义filter-method来实现基于拼音的匹配逻辑。
* 拼音转换：使用pinyin库将选项标签转换为拼音，以辅助搜索, 例如：options中有一个`label`为`"深圳"`，则可以通过`sz`来进行搜索。
* 高亮匹配：在搜索结果中匹配到的部分会以<span class="highlight">...</span>包裹，用于样式高亮显示, 支持非连续字符串的高亮。

## 使用方式

**安装依赖**
```bash
# 使用npm
npm install el-pro-select 

# 使用yarn 
yarn add el-pro-select

# 使用pnpm
pnpm add el-pro-select
```

**使用组件**
```js 
// main.js
import { createApp } from 'vue'
import './style.css'
import App from './App.vue'
import ElProSelect from 'el-pro-select' // 引入组件
import 'el-pro-select/style' // 引入样式

const app = createApp(App)
app.use(ElProSelect)
app.mount('#app')

```

**示例** 
![1](https://github.com/JOU-amjs/sdm2/assets/29848971/f7f5fd21-d49b-45b6-94d4-e94c25326f0c)