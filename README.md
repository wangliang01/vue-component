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