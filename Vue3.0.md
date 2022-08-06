# 1.vue 基础入门

## 1.vue 简介

### 1.解读核心关键词

官方给 vue 的定位是**前端框架**，因为它**提供了构建用户界面的一整套解决方案**（俗称 vue 全家桶）：

- vue（核心库）
- vue-router（路由方案）
- vuex（状态管理方案）
- vue 组件库（快速搭建页面 UI 效果的方案）

以及**辅助 vue 项目开发**的一系列工具：

- vue-cli（npm 全局包：一键生成工程化的 vue 项目 - 基于 webpack、大而全）
- vite（npm 全局包：一键生成工程化的 vue 项目 - 小而巧）
- vue-devtools（浏览器插件：辅助调试的工具）
- vetur（vscode 插件：提供语法高亮和智能提示）

### 2.vue2.x 和 vue3.x 版本的对比

vue2.x 中**绝大多数的 API 与特性**，在 vue3.x 中**同样支持**。同时，vue3.x 中还**新增了 3.x 所特有的功能**、并**废弃了某些 2.x 中的旧功能**：

新增的功能例如：

- **组合式 API**、多根节点组件、更好的 TypeScript 支持等

废弃的旧功能如下：

- **过滤器**、不再支持 $on，$off 和 $once 实例方法等

详细的变更信息，请参考官方文档给出的迁移指南：

https://v3.cn.vuejs.org/guide/migration/introduction.html

## 2.vue 的调试工具

### 1.安装 vue-devtools 调试工具

**Chrome 浏览器**在线安装 vue-devtools

vue 2.x 调试工具：

- https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd

vue 3.x 调试工具：

- https://chrome.google.com/webstore/detail/vuejs-devtools/ljjemllljcmogpfapbkkighbhhppjdbg

> 注意：vue2 和 vue3 的浏览器调试工具不能交叉使用！

# 2.组件基础（上）

## 1.vite 的基本使用

### 1.如何快速创建 vue 的 SPA 项目

vue 官方提供了**两种**快速创建工程化的 SPA 项目的方式：

1. 基于 **vite** 创建 SPA 项目
2. 基于 **vue-cli** 创建 SPA 项目

![](./Vue3.0/如何快速创建vue的SPA项目.png)

### 2.创建 vite 的项目

按照顺序执行如下的命令，即可基于 vite 创建 vue 3.x 的工程化项目：

```bash
npm init vite-app 项目名称
cd 项目名称
npm i
npm run dev
```

### 3.梳理项目的结构

使用 vite 创建的项目结构如下：

![](./Vue3.0/梳理项目的结构.png)

其中：

- node_modules 目录用来存放第三方依赖包
- public 是公共的静态资源目录
- **src** 是项目的源代码目录（程序员写的所有代码都要放在此目录下）
- .gitignore 是 Git 的忽略文件
- **index.html** 是 SPA 单页面应用程序中唯一的 HTML 页面
- package.json 是项目的包管理配置文件

在 **src** 这个项目源代码目录之下，包含了如下的文件和文件夹：

![](./Vue3.0/梳理项目的结构2.png)

其中：

- **assets** 目录用来存放项目中所有的**静态资源文件**（css、fonts等）
- **components** 目录用来存放项目中所有的**自定义组件**
- **App.vue** 是项目的**根组件**
- **index.css** 是项目的**全局样式表**文件
- **main.js** 是整个项目的**打包入口文件**

### 4.vite 项目的运行流程

在工程化的项目中，vue 要做的事情很单纯：通过 **main.js** 把 **App.vue** 渲染到 **index.html** 的指定区域中。

其中：

1. **App.vue** 用来编写待渲染的**模板结构**
2. **index.html** 中需要预留一个 **el 区域**
3. **main.js** 把 App.vue 渲染到了 index.html 所预留的区域中

#### 1.在 App.vue 中编写模板结构

清空 App.vue 的默认内容，并书写如下的模板结构：

```vue
<template>
  <div class="app-container">
    <h3>这是 App 根组件</h3>
  </div>
</template>
```

#### 2.在 index.html 中预留 el 区域

打开 index.html 页面，确认预留了 el 区域：

```html
<!-- id 为 app 的 div，就是将来 vue 要控制的区域 -->
<div id="app"></div>
<script type="module" src="/src/main.js"></script>
```

#### 3.在 main.js 中进行渲染

按照 **vue 3.x** 的**标准用法**，把 **App.vue 中的模板内容**渲染到 **index.html 页面的 el 区域**中：

```js
// 1. 从 vue 中按需导入 createApp 函数
// createApp 函数的作用：创建 vue 的 “单页面应用程序实例”
import { createApp } from 'vue'
// 2. 导入待渲染的 App 组件
import App from './App.vue'

// 3. 调用 createApp() 函数，返回值是 “单页面应用程序的实例”，同时把 App 组件作为参数传给 createApp 函数，表示要把 App 渲染到 index.html 页面上
const vue = createApp(App)

// 4. 调用 “单页面应用程序实例” 的 mount 方法，用来指定 vue 实例要控制的区域
vue.mount('#app')
```

## 2.vue 组件的构成

### 1 在 template 中定义根节点

在 **vue 2.x** 的版本中，`<template>` 节点内的 DOM 结构仅支持**单个根节点**：

```vue
<template>
  <div class="app-container">
    <h3>这是 App 根组件</h3>
  </div>
</template>
```

但是，在 **vue 3.x** 的版本中，`<template>` 中支持定义**多个根节点**：

```vue
<template>
  <!-- 在 vue 3.x 的版本中，<template> 中支持定义多个根节点 -->
  <h3>这是 App 根组件</h3>
  <h3>这是 App 的第二个根节点</h3>
</template>
```

### 2.让 style 中支持 less 语法

安装依赖包：

```bash
npm i less -D
```

在 `<style>` 标签上添加 **lang="less"** 属性，即可使用 less 语法编写组件的样式：

```vue
<style lang="less">
  div {
    background-color: skyblue;

    span {
      color: pink;
    }
  }
</style>
```

## 3.组件的基本使用

### 1.使用全局注册组件

使用 app.component() 方法注册的全局组件，**直接以标签的形式进行使用**即可，例如：

```js
import Count from "@/components/Count.vue";
Vue.component("Count", Count);// 第一个参数是使用这个组件时用的标签名
```

### 2.Class 与 Style 绑定

在实际开发中经常会遇到**动态操作元素样式**的需求。因此，vue 允许开发者通过 **v-bind** 属性绑定指令，为元素动态绑定 **class 属性的值**和**行内的 style 样式**。

#### 1.动态绑定 HTML 的 class

可以通过**三元表达式，动态的为元素绑定 class 的类名**。示例代码如下：

```vue
<template>
  <div :class="isItalic ? 'italic' : ''">动态绑定 HTML 的 class</div>
  <button @click="isItalic = !isItalic">改变 isItalic 的值</button>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      isItalic: true
    }
  }
}
</script>

<style lang="less" scoped>
.italic {
  font-style: italic;
}
</style>
```

#### 2.以数组语法绑定 HTML 的 class

如果元素需要动态**绑定多个** class 的类名，此时可以使用**数组的语法格式**：

```vue
<template>
  <div :class="[isItalic ? 'italic' : '', isRed ? 'red': '']">以数组语法绑定 HTML 的 class</div>
  <button @click="isItalic = !isItalic">改变 isItalic 的值</button>
  <button @click="isRed = !isRed">改变 isRed 的值</button>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      isItalic: true,
      isRed: true
    }
  }
}
</script>

<style lang="less" scoped>
.italic {
  font-style: italic;
}
.red {
  color: red;
}
</style>
```

#### 3.以对象语法绑定 HTML 的 class

使用**数组语法**动态绑定 class 会导致**模板结构臃肿**的问题。此时可以使用**对象语法**进行**简化**：

```vue
<template>
  <div :class="classObj">以对象语法绑定 HTML 的 class</div>
  <button @click="classObj.italic = !classObj.italic">改变 classObj.isItalic 的值</button>
  <button @click="classObj.red = !classObj.red">改变 classObj.isRed 的值</button>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      // 对象中，属性名是 class 类名，值是布尔值
      classObj: {
        italic: true,
        red: true
      }
    }
  }
}
</script>

<style lang="less" scoped>
.italic {
  font-style: italic;
}
.red {
  color: red;
}
</style>
```

#### 4.以对象语法绑定内联的 style

**:style** 的**对象语法**十分直观——看着非常像 CSS，但其实是一个 **JavaScript 对象**。CSS property 名可以用驼峰式（camelCase）或短横线分隔（kebab-case，记得用引号括起来）来命名：

```vue
<template>
  <div :style="{ color: 'skyblue', fontSize: '30px', 'background-color': 'black' }">以对象语法绑定内联的 style</div>
</template>
```

# 3.组件基础（下）

## 1.props 验证

**对象类型的 props 节点**提供了多种数据验证方案，例如：

1. 基础的类型检查
2. 多个可能的类型
3. 必填项校验
4. 属性默认值
5. 自定义验证函数

### 1.基础的类型检查

可以直接为组件的 prop 属性指定**基础的校验类型**，从而防止**组件的使用者**为其绑定**错误类型的数据**：

```vue
<script>
export default {
  props: {
    args1: String,// 字符串类型
    args2: Number,// 数字类型
    args3: Boolean,// 布尔类型
    args4: Array,// 数组类型
    args5: Object,// 对象类型
    args6: Date,// 日期类型
    args7: Function,// 函数类型
    args8: Symbol// 符号类型
  }
}
</script>
```

### 2.多个可能的类型

如果某个 prop 属性值的**类型不唯一**，此时可以通过数组的形式，为其指定多个可能的类型，示例代码如下：

```vue
<script>
export default {
  props: {
    args: [String, Number]// 字符串或数字类型
  }
}
</script>
```

### 3.必填项校验

如果**组件的某个 prop 属性是必填项**，必须让组件的使用者为其传递属性的值。此时，可以通过如下的方式将其设置为必填项：

```vue
<script>
export default {
  props: {
    args: {
      type: String,
      required: true// 当前属性的值是必填项，如果使用者没指定 args 属性的值，则在终端进行警告提示
    }
  }
}
</script>
```

### 4.属性默认值

在封装组件时，可以为某个 prop 属性**指定默认值**。示例代码如下：

```vue
<script>
export default {
  props: {
    args: {
      default: 'aaa'// 如果使用者没有指定 args 的值，则 args 的值默认为 aaa
      type: String
    }
  }
}
</script>
```

### 5.自定义验证函数

在封装组件时，可以为 prop 属性指定**自定义的验证函数**，从而**对 prop 属性的值进行更加精确的控制**：

```vue
<script>
export default {
  props: {
    args: {
      // 通过 validator 函数，对 args 属性的值进行校验，“属性的值” 可以通过形参 value 进行接收
      validator(value) {
        console.log(value)
        // 返回值为 true 表示验证通过，false 表示验证失败，终端会提示警告
        return value === 'aaa'
      }
    }
  }
}
</script>
```

## 2.组件上的 v-model

### 1.为什么需要在组件上使用 v-model

v-model 是双向数据绑定指令，当**需要维护组件内外数据的同步**时，可以在组件上使用 v-model 指令。示意图如下：

![](./Vue3.0/为什么需要在组件上使用v-model.png)

- **外界数据的变化**会**自动同步**到 counter 组件中
- counter 组件中数据的变化，也会**自动同步到外界**

### 2.在组件上使用 v-model 的步骤

![](./Vue3.0/在组件上使用v-model的步骤.png)

1. 父组件通过 **v-bind:** 属性绑定的形式，把数据传递给子组件
2. 子组件中，通过 **props** 接收父组件传递过来的数据

![](./Vue3.0/在组件上使用v-model的步骤2.png)

1. 在 v-bind: 指令之前添加 **v-model** 指令
2. 在子组件中声明 **emits** 自定义事件，格式为 **update:**xxx
3. 调用 **$emit()** 触发自定义事件，更新父组件中的数据

# 4.组件高级（上）

## 1.组件的生命周期

### 1.组件中主要的生命周期函数

| 生命周期函数  | 执行时机                     | 所属阶段 | 执行次数 | 应用场景             |
| ------------- | ---------------------------- | -------- | -------- | -------------------- |
| **created**   | 组件在内存中创建完毕后       | 创建阶段 | 唯一1次  | 发 ajax 请求初始数据 |
| **mounted**   | 组件初次在页面中渲染完毕后   | 创建阶段 | 唯一1次  | 操作 DOM 元素        |
| **updated**   | 组件在页面中被重新渲染完毕后 | 运行阶段 | 0或多次  | -                    |
| **unmounted** | 组件被销毁后（页面和内存）   | 销毁阶段 | 唯一1次  | -                    |

> 注意：在实际开发中，**created** 是**最常用的**生命周期函数！

### 2.组件中全部的生命周期函数

| 生命周期函数  | 执行时机                     | 所属阶段 | 执行次数 | 应用场景             |
| ------------- | ---------------------------- | -------- | -------- | -------------------- |
| beforeCreate  | 在内存中开始创建组件之前     | 创建阶段 | 唯一1次  | -                    |
| **created**   | 组件在内存中创建完毕后       | 创建阶段 | 唯一1次  | 发 ajax 请求初始数据 |
| beforeMount   | 在把组件初次渲染到页面之前   | 创建阶段 | 唯一1次  | -                    |
| **mounted**   | 组件初次在页面中渲染完毕后   | 创建阶段 | 唯一1次  | 操作 DOM 元素        |
| beforeUpdate  | 在组件被重新渲染之前         | 运行阶段 | 0或多次  | -                    |
| **updated**   | 组件在页面中被重新渲染完毕后 | 运行阶段 | 0或多次  | -                    |
| beforeUnmount | 在组件被销毁之前             | 销毁阶段 | 唯一1次  | -                    |
| **unmounted** | 组件被销毁后（页面和内存）   | 销毁阶段 | 唯一1次  | -                    |

> 疑问：为什么不在 **beforeCreate** 中发 ajax 请求初始数据？

### 3.完整的生命周期图示

可以参考 vue 官方文档给出的 “**生命周期图示**”，进一步理解组件生命周期执行的过程：

https://v3.cn.vuejs.org/guide/instance.html#%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%9B%BE%E7%A4%BA

![](./Vue3.0/lifecycle.svg)

## 2.组件之间的数据共享

### 1.兄弟组件之间的数据共享

**兄弟组件之间**实现数据共享的方案是 **EventBus**。可以借助于第三方的包 **mitt** 来创建 **eventBus** 对象，从而实现兄弟组件之间的数据共享。示意图如下：

![](./Vue3.0/兄弟组件之间的数据共享.png)

在项目中运行如下的命令，安装 mitt 依赖包：

```bash
npm i mitt
```

兄弟组件 A（发送方）：

```vue
<script>
import bus from './eventBus.js'

export default {
  data() {
    return {
      msg: "Hello Right.vue"
    }
  },
  methods: {
    sendMsg() {
      // 发送数据给兄弟组件，注意：不要 $ 符号
      bus.emit('share', this.msg)
    }
  }
}
</script>
```

eventBus.js：

```js
import mitt from 'mitt'

const bus = mitt()

export default bus
```

兄弟组件 B（接收方）：

```vue
<script>
import bus from './eventBus.js'

export default {
  created() {
    // 接收兄弟组件发送过来的数据，注意：不要 $ 符号
    bus.on('share', val => this.msgFromLeft = val)
  },
  data() {
    return {
      msgFromLeft: '',
    };
  }
}
</script>
```

### 2.后代关系组件之间的数据共享

后代关系组件之间共享数据，指的是**父节点的组件**向其**子孙组件**共享数据。此时组件之间的嵌套关系比较复杂，可以使用 **provide** 和 **inject** 实现后代关系组件之间的数据共享。

#### 1.父节点通过 provide 共享数据

父节点的组件可以通过 **provide 方法**，对其**子孙组件**共享数据：

```vue
<script>
export default {
  name: 'App',
  // provide 函数 return 的对象中，包含了 “要向子孙组件共享的数据”
  provide() {
    return {
      message: this.message
    }
  },
  data() {
    return {
      message: 'Hello'
    }
  }
}
</script>
```

#### 2.子孙节点通过 inject 接收数据

子孙节点可以使用 **inject** 数组，接收父级节点**向下共享的数据**。示例代码如下：

```vue
<template>
  <div class="left-son-container">
    <h3>这是 LeftSon.vue 组件</h3>
    <p>App.vue 祖宗节点向下共享的 message 数据：{{ message }}</p>
  </div>
</template>

<script>
export default {
  // 接收 App.vue 祖宗节点向下共享的 message 数据
  inject: ['message']
}
</script>
```

#### 3.父节点对外共享响应式的数据

父节点使用 provide 向下共享数据时，可以结合 **computed 函数**向下共享**响应式的数据**。示例代码如下：

```vue
<script>
import { computed } from 'vue'

export default {
  name: 'App',
  provide() {
    return {
      // 共享响应式的数据
      color: computed(() => this.color)
    }
  },
  data() {
    return {
      color: 'pink'
    }
  }
}
</script>
```

#### 4.子孙节点使用响应式的数据

如果父级节点共享的是**响应式的数据**，则子孙节点必须以 .value 的形式进行使用。示例代码如下：

```vue
<template>
  <div class="left-son-container">
    <h3>这是 LeftSon.vue 组件</h3>
    <p>App.vue 祖宗节点向下共享的 color 数据：{{ color.value }}</p>
  </div>
</template>

<script>
export default {
  // 接收 App.vue 祖宗节点向下共享的 color 数据
  inject: ['color']
}
</script>
```

## 3.vue 3.x 中全局配置 axios

### 1.为什么要全局配置 axios

在实际项目开发中，几乎每个组件中都会用到 axios 发起数据请求。此时会遇到如下两个问题：

1. 每个组件中都需要**导入 axios**（代码臃肿）
2. 每次发请求都需要填写**完整的请求路径**（不利于后期的维护）

![](./Vue3.0/为什么要全局配置axios.png)

### 2.如何全局配置 axios

在 **main.js** 入口文件中，通过 **app.config.globalProperties** 全局挂载 axios，示例代码如下：

```js
// 导入 axios
import axios from 'axios'

// 为 axios 配置请求的根路径
axios.defaults.baseURL = 'https://www.escook.cn/api'

// 将 axios 挂载为 vue 的全局自定义属性
vue.config.globalProperties.$http = axios
```

在组件中使用：

```vue
<script>
export default {
  created() {
    // 测试 axios
    this.$http.get('/cart').then(response => console.log(response.data))
  }
}
</script>
```

# 5.组件高级（下）

## 1.自定义指令

【bind 改成了 **mounted**】【update 改成了 **updated**】，其他根 vue2 一样

# 6.路由

## 1.vue-router 的基本使用

### 1.vue-router 的版本

vue-router 目前有 **3.x** 的版本和 **4.x** 的版本。其中：

- vue-router 3.x 只能结合 **vue2** 进行使用
- vue-router 4.x 只能结合 **vue3** 进行使用

vue-router 的官方文档地址：https://router.vuejs.org/zh/

### 2.vue-router 4.x 的基本使用步骤

#### 1.在项目中安装 vue-router

在 vue3 的项目中，只能安装并使用 vue-router 4.x。安装的命令如下：

```bash
npm i vue-router
```

#### 2.创建路由模块

在 **src** 源代码目录下，新建 **router/index.js** 路由模块，并初始化如下的代码：

```js
// 1. 从 vue-router 中按需导入两个方法
// createRouter 方法用于创建路由的实例对象
// createWebHashHistory 用于指定路由的工作模式（hash 模式）
import { createRouter, createWebHashHistory } from 'vue-router'

// 2. 创建路由的实例对象
const router = new createRouter({
  // 3. 通过 history 属性指定路由的工作模式
  history: createWebHashHistory()
})

// 4. 向外共享路由的实例对象
export default router
```

#### 3.导入并挂载路由模块

在 src/**main.js** 入口文件中，导入并挂载路由模块。示例代码如下：

```js
import { createApp } from 'vue';
import App from './App.vue';
import './index.css';
// 导入路由模块
import router from './components/router/index.js'

const vue = createApp(App);

// 挂载路由模块
vue.use(router)

vue.mount('#app');
```

#### 4.声明路由链接和占位符

在 src/App.vue 组件中，使用 vue-router 提供的 **`<router-link>`** 和 **`<router-view>`** 声明路由链接和占位符：

```vue
<template>
  <!-- 1. 定义路由的占位符，# 省略 -->
  <router-link to="/home">首页</router-link>
  <router-link to="/movie">电影</router-link>
  <router-link to="/about">关于</router-link>
  <!-- 2. 定义路由的占位符 -->
  <router-view />
</template>
```

#### 5.声明路由的匹配规则

在 src/router/index.js 路由模块中，通过 **routes 数组**声明路由的匹配规则。示例代码如下：

```js
// 导入需要使用路由切换展示的组件
import Home from '../Home.vue'
import Movie from '../Movie.vue'
import About from '../About.vue'

const router = new createRouter({
  history: createWebHashHistory(),
  // 声明路由规则
  routes: [
    { path: '/home', component: Home },
    { path: '/movie', component: Movie },
    { path: '/about', component: About }
  ]
})
```

## 2.vue-router 的高级用法

### 1.路由高亮

可以通过如下的两种方式，将**激活的路由链接**进行高亮显示：

1. 使用**默认的**高亮 class 类
2. **自定义**路由高亮的 class 类

#### 1.默认的高亮 class 类

被激活的路由链接，默认会应用一个叫做 **router-link-active** 的类名。开发者可以使用此**类名选择器**，为**激活的路由链接**设置高亮的样式：

```vue
<style lang="less" scoped>
.router-link-active {
  background-color: red;
  color: #fff;
  font-weight: bold;
}
</style>
```

#### 2.自定义路由高亮的 class 类

在创建路由的实例对象时，开发者可以基于 **linkActiveClass** 属性，自定义路由链接被激活时所应用的类名：

```js
const router = new createRouter({
  // 默认的 router-link-active 路由高亮类名会被覆盖掉，改为 router-active
  linkActiveClass: 'router-active',
})
```

### 2.命名路由

通过 **name 属性**为路由规则**定义名称**的方式，叫做**命名路由**。示例代码如下：

```js
const router = new createRouter({
  routes: [
    // 使用 name 属性为当前路由规则定义一个 “名称”
    { name: 'movie', path: '/movie/:id', component: Movie }
  ]
})
```

> 注意：命名路由的 **name 值不能重复，必须保证唯一性**！

#### 1.使用命名路由实现声明式导航

为 `<router-link>` 标签动态绑定 to 属性的值，并通过 **name 属性**指定要跳转到的路由规则。期间还可以用 **params 属性**指定跳转期间要携带的路由参数。示例代码 如下：

```vue
<template>
	<h3>App 组件</h3>
  <!-- 使用命名路由实现声明式导航，相当于 to="/movie/4" -->
  <router-link :to="{ name: 'movie', params: {id: 4} }">电影4</router-link>
</template>
```

#### 2.使用命名路由实现编程式导航

调用 **push 函数**期间指定一个**配置对象，name** 是要跳转到的路由规则、**params** 是携带的路由参数：

```vue
<template>
  <div class="home-container">
    <h3>Home 组件</h3>
    <!-- 使用命名路由实现编程式导航 -->
    <button @click="$router.push({ name: 'movie', params: {id: 4} })">跳转到电影4</button>
  </div>
</template>
```

# 7.vue 基础 - 综合案例

## 1.组件库

### 1.什么是 vue 组件库

在实际开发中，前端开发者可以把**自己封装的 .vue 组件**整理、打包、并**发布为 npm 的包**，从而供其他人下载和使用。这种可以直接下载并在项目中使用的现成组件，就叫做 vue **组件库**。

### 2.vue 组件库和 bootstrap 的区别

二者之间存在本质的区别：

- bootstrap 只提供了**纯粹的原材料**（css 样式、HTML 结构以及 JS 特效），需要由开发者做**进一步的组装**和**改造**
- vue 组件库是**遵循 vue 语法、高度定制**的现成组件，开箱即用

### 3.最常用的 vue 组件库

1. **PC 端**
   - Element UI（https://element.eleme.cn/#/zh-CN）
   - View UI（http://v1.iviewui.com/）
2. **移动端**
   - Vant（https://vant-contrib.gitee.io/vant/v4/#/zh-CN）
   - Mint UI（http://mint-ui.github.io/#!/zh-cn）

### 4.Element UI

Element UI 是**饿了么前端团队**开源的一套 **PC 端 vue 组件库**。支持在 vue2 和 vue3 的项目中使用：

- **vue2** 的项目使用**旧版的** Element UI（https://element.eleme.cn/#/zh-CN）
- **vue3** 的项目使用**新版的** Element Plus（https://element-plus.gitee.io/zh-CN/）

## 2.axios 拦截器

### 1.什么是拦截器

**拦截器**（英文：Interceptors）会在**每次发起 ajax 请求**和**得到响应**的时候自动被触发。

![](./Vue3.0/什么是拦截器.png)

应用场景：

1. Token 身份认证
2. Loading 效果
3. etc...

### 2.配置请求拦截器

通过 **axios.interceptors.request.use(成功的回调, 失败的回调)** 可以配置请求拦截器。示例代码如下：

```js
// 配置请求拦截器
axios.interceptors.request.use(config => {
  // Do something before request is sent
  return config
}, error => {
  // Do something with request error
  return Promise.reject(error)
})
```

> 注意：**失败的回调函数可以被省略**！

#### 1.请求拦截器 – Token 认证

```js
// 导入 axios
import axios from 'axios'

// 为 axios 配置请求的根路径
axios.defaults.baseURL = 'https://www.escook.cn'

// 配置请求拦截器
axios.interceptors.request.use(config => {
  // 为当前请求配置 Token 认证字段
  config.headers.Authorization = 'Bearer xxx'
  return config
})

// 将 axios 挂载为 vue 的全局自定义属性
vue.config.globalProperties.$http = axios
```

#### 2.请求拦截器 – 展示 Loading 效果

借助于 element-plus 提供的 **Loading 效果**组件（https://element-plus.gitee.io/zh-CN/component/loading.html#%E4%BB%A5%E6%9C%8D%E5%8A%A1%E7%9A%84%E6%96%B9%E5%BC%8F%E6%9D%A5%E8%B0%83%E7%94%A8）可以方便的实现 Loading 效果的展示：

```js
// 按需导入 Loading 效果组件
import { ElLoading } from 'element-plus'

// 声明变量，用来存储 ElLoading 组件的实例对象
let loadingInstance = null

// 配置请求拦截器
axios.interceptors.request.use(config => {
  // 调用 ElLoading 组件的 service() 方法，创建 Loading 组件的实例，并全屏展示 loading 效果
  loadingInstance = ElLoading.service({ fullscreen: true })
  return config
})
```

### 3.配置响应拦截器

通过 **axios.interceptors.response.use(成功的回调, 失败的回调)** 可以配置响应拦截器。示例代码如下：

```js
配置响应拦截器
axios.interceptors.response.use(response => {
  // Any status code that lie within the range of 2xx cause this function to trigger
  // Do something with response data
  return response
}, error => {
  // Any status code that falls outside the range of 2xx cause this function to trigger
  // Do something with response error
  return Promise.reject(error)
})
```

> 注意：**失败的回调函数可以被省略**！

#### 1.响应拦截器 – 关闭 Loading 效果

调用 **ElLoading 实例**提供的 **close()** 方法即可**关闭 Loading 效果**，示例代码如下：

```js
// 配置响应拦截器
axios.interceptors.response.use(response => {
  // 调用 ElLoading 实例的 close() 方法即可关闭 Loading 效果
  loadingInstance.close()
  return response
})
```

## 3.proxy 跨域代理

### 1.回顾：接口的跨域问题

vue 项目运行的地址：http://localhost:8080/

API 接口运行的地址：https://www.escook.cn/api/users

由于当前的 API 接口**没有开启 CORS** 跨域资源共享，因此默认情况下，上面的接口**无法请求成功**！

![](./Vue3.0/回顾：接口的跨域问题.png)

### 2.通过代理解决接口的跨域问题

通过 vue-cli 创建的项目在遇到接口跨域问题时，可以通过**代理**的方式来解决：

![](./Vue3.0/通过代理解决接口的跨域问题.png)

1. 把 axios 的**请求根路径**设置为 **vue 项目的运行地址**（接口请求不再跨域）
2. vue 项目发现请求的接口不存在，把请求**转交给 proxy 代理**
3. 代理把请求根路径**替换为** devServer.proxy 属性的值，**发起真正的数据请求**
4. 代理把请求到的数据，**转发给 axios**

### 3.在项目中配置 proxy 代理

步骤1，在 **main.js** 入口文件中，把 **axios 的请求根路径**改造为**当前 web 项目的根路径**：

```js
// 把 https://www.escook.cn 改成了 http://localhost:8080
axios.defaults.baseURL = 'http://localhost:8080'
```

步骤2，在**项目根目录**下创建 **vue.config.js** 的配置文件，并声明如下的配置：

```js
const { defineConfig } = require('@vue/cli-service')

module.exports = defineConfig({
  transpileDependencies: true,
  // 通过代理解决接口的跨域问题
  devServer: {
    // 当项目在开发调式阶段，会将任何未知请求（没有匹配到静态文件的请求）代理到 https://www.escook.cn
    proxy: 'https://www.escook.cn'
  }
})
```

> 注意：
>
> 1. **devServer.proxy** 提供的代理功能，**仅在开发调试阶段生效**
> 2. 项目上线发布时，依旧需要 API 接口服务器**开启 CORS** 跨域资源共享

# 3.Vuex

## 1.Vuex 概述

### 1.组件之间共享数据的方式

父向子传值：**v-bind 属性绑定**

子向父传值：**v-on 事件绑定**

- $on 接收数据的那个组件
- $emit 发送数据的那个组件

### 2.Vuex 是什么

**Vuex** 是实现组件全局状态（数据）管理的一种机制，可以方便的实现组件之间数据的共享。

在企业级的 vue 项目开发中，vuex 可以让组件之间的数据共享变得**高效、清晰**、且**易于维护**。

![](./Vue3.0/vuex.png)

### 3.使用 Vuex 统一管理状态的好处

1. 能够在 vuex 中集中管理共享的数据，易于开发和后期维护
2. 能够高效地实现组件之间的数据共享，提高开发效率
3. 存储在 vuex 中的数据都是响应式的，能够实时保持数据与页面的同步

### 4.什么样的数据适合存储到 Vuex 中

一般情况下，只有组件之间共享的数据，才有必要存储到 vuex 中；对于组件中的私有数据，依旧存储在组件自身的 data 中即可。

## 2.Vuex 的基本使用

### 1.安装 vuex 依赖包

```bash
npm i vuex
```

### 2.导入 vuex 包

```js
import { createStore } from 'vuex'
```

### 3.创建 store 对象

```js
// 创建 store 数据源，提供唯一的公共数据
export default createStore({
  // state 中存放的就是全局共享的数据
  state: {
    count: 0
  }
})
```

### 4.将 store 对象挂载到 vue 实例中

```js
import { createApp } from 'vue'
import App from './App.vue'
import store from './store'

// 将创建的共享数据对象，挂载到 Vue 实例中
// 所有的组件，就可以直接从 store 中获取全局的数据了
createApp(App).use(store).mount('#app')
```

## 3.Vuex 的核心概念

### 1.核心概念概述

Vuex 中的主要核心概念如下：

- State
- Mutation
- Action
- Getter

### 2.State

State 提供唯一的公共数据源，所有共享的数据都要统一放到 Store 的 State 中进行存储。

定义 state：

```js
export default createStore({
  // state 中存放的就是全局共享的数据
  state: {
    count: 0
  }
})
```

**访问 state 中数据的第一种方式**

```js
// 访问 count
this.$store.state.count
```

**访问 state 中数据的第二种方式**

```vue
<script>
// 1. 从 vuex 中按需导入 mapState 函数
import { mapState } from 'vuex'

export default {
  computed: {
    // 2. 将全局数据，映射为当前组件的计算属性
    ...mapState(['count'])
  }
}
</script>
```

### 3.Mutation

Mutation 用于变更 Store 中的数据。

1. 只能通过 Mutation 变更 Store 数据，不可以直接操作 Stroe 中的数据。
2. 通过这种方式虽然操作起来稍微繁琐一些，但是可以集中监控所有数据的变化。

**触发 mutations 的第一种方式**

定义 mutations：

```js
export default createStore({
  // mutations 中的函数用于变更 state 中的数据
  mutations: {
    // 定义 mutation 函数 add
    add(state) {
      state.count++
    }
  }
})
```

触发 mutations：

```js
// 调用 mutations 里的 add() 函数
this.$store.commit('add')
```

可以在触发 mutations 时传递参数：

```js
export default createStore({
  mutations: {
    // 传递参数，step 是传递过来的参数
    addN(state, step) {
      state.count += step
    }
  }
})
```

触发 mutations：

```js
// 调用 mutations 里的 addN() 函数，并传递参数 5
this.$store.commit('addN', 5)
```

**触发 mutations 的第二种方式**

```vue
<script>
// 1. 从 vuex 中按需导入 mapMutations 函数
import { mapMutations } from 'vuex'

export default {
  methods: {
    // 2. 将指定的 actions 函数，映射为当前组件的 methods 函数
    ...mapActions(['addAsync', 'addNAsync'])
  }
}
</script>
```

### 4.Action

Action 用于处理异步任务。

如果通过异步操作变更数据，必须通过 Action，而不能使用 Mutation，但是在 Action 中还是要通过触发 Mutation 的方式间接变更数据。

**触发 actions 的第一种方式**

定义 actions：

```js
export default createStore({
  mutations: {
    add(state) {
      state.count++
    }
  },
  // actions 中的函数用于处理异步任务
  actions: {
    addAsync(context) {
      // 1 秒后调用 mutations 里的 add() 函数
      setTimeout(() => context.commit('add'), 1000)
    }
  }
})
```

触发 actions：

```js
// 调用 actions 里的 addAsync() 函数
this.$store.dispatch('addAsync')
```

触发 actions 异步任务时携带参数：

```js
export default createStore({
  mutations: {
    addN(state, step) {
      state.count += step
    }
  },
  // actions 中的函数用于处理异步任务
  actions: {
    addNAsync(context, step) {
      setTimeout(() => context.commit('addN', step), 1000)
    }
  }
})
```

触发 actions：

```js
// 调用 actions 里的 addNAsync() 函数，并传递参数 5
this.$store.dispatch('addNAsync', 5)
```

**触发 actions 的第二种方式**

```vue
<script>
// 1. 从 vuex 中按需导入 mapActions 函数
import { mapActions } from 'vuex'

export default {
  methods: {
    // 2. 将指定的 actions 函数，映射为当前组件的 methods 函数
    ...mapActions(['addAsync', 'addNAsync'])
  }
}
</script>
```

### 5.Getter

Getter 用于对 Store 中的数据进行加工处理形成新的数据。

1. Getter 可以对 Store 中已有的数据加工处理之后形成新的数据，类似 Vue 的计算属性。
2. Store 中数据发生变化，Getter 的数据也会跟着变化。

定义 getters：

```js
export default createStore({
  state: {
    count: 0
  },
  // getters 用于对 state 中的数据进行加工处理形成新的数据
  getters: {
    getCount(state) {
      return `当前最新的数量是【${state.count}】`
    }
  }
})
```

**访问 getters 的第一种方式**

```js
// 访问 getCount()
this.$store.getters.getCount
```

**访问 getters 的第二种方式**

```vue
<script>
// 1. 从 vuex 中按需导入 mapGetters 函数
import { mapGetters } from 'vuex'

export default {
  computed: {
    // 2. 将指定的 getters 函数，映射为当前组件的计算属性
    ...mapGetters(['getCount'])
  }
}
</script>
```
