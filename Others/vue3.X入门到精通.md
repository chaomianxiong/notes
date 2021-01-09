# Vue3 核心技术新特性看下图:

![图片](https://gitee.com/wq6195/pic-bed/raw/master/img/20210107141725.webp)

**刚开始用vue3的感觉:**

“太失望了。杂七杂八一堆丢在 setup 里，我还不如直接用 react”
我的天，3.0 这么搞的话，代码结构不清晰，语义不明确，无异于把 vue 自身优点都扔了怎么感觉代码结构上没有 2.0 清晰了呢 这要是代码量上去了是不是不好维护啊!





**深入了解后:**

*大如 Vue3 这种全球热门的框架，任何一个 `breaking-change` 的设计一定有它的深思熟虑和权衡，那么 `composition-api` 出现是为了解决什么问题呢？这是一个我们需要首先思考明白的问题。*

**首先抛出 Vue2 的代码模式下存在的几个问题。**

1. 随着功能的增长，复杂组件的代码变得越来越难以维护。尤其发生你去新接手别人的代码时。根本原因是 Vue 的现有 API 通过「选项」组织代码，但是在大部分情况下，通过逻辑考虑来组织代码更有意义。
2. 缺少一种比较「干净」的在多个组件之间提取和复用逻辑的机制。
3. 类型推断不够友好。

**以下是我写的vue3.0教程:**

# vue3.0入门到精通

## vue3.0 安装



前安装过vue的2.0版本，你需要把2.0相关的删除

```
npm uni -g vue-cli
```

安装vue/cli脚架

```
npm i -g @vue/cli
```

检查版本号,目前安装vuecli 4.5.4

```
vue -V
```

创建:在命令窗口输入指令

选择default vue 3

```
vue create 项目名称
```

## vue composition API





vue3.0 侧重于解决代码组织与逻辑复用问题

目前，我们使用的是“options”API 构建组件。 为了将逻辑添加到Vue组件中，我们填充（options）属性，如data、methods、computed等。 这种方法最大的缺点是，它本身不是一个工作的JavaScript代码。 您需要确切地知道模板中可以访问哪些属性以及this关键字的行为。在底层，Vue编译器需要将此属性转换为工作代码。正因为如此，我们无法从自动建议或类型检查中获益。

Composition API希望将通过当前组件属性、可用的机制公开为JavaScript函数来解决这个问题。 Vue核心团队将组件Composition API描述为“一套附加的、基于函数的api，允许灵活地组合组件逻辑”。 使用Composition API编写的代码更易读，并且场景不复杂，这使得阅读和学习变得更容易。

让我们看到一个非常简单的组件示例，它使用新的组件Composition API来理解它是如何工作的。

```vue
<template>
<div id="app">
  <img alt="Vue logo" src="./assets/logo.png">
  <div>{{msg}}年龄为{{age}}</div>
  <button @click="add"> + </button>
</div>
</template>

<script>

export default {
name: 'App',
data() {
  return {
    msg:'王大合',
    age:18
  }
},
methods:{
  add() {
    this.age += 1
  }
}

}
</script>
```



##### setup

vue3.0将组件的逻辑都写在了函数内部,setup()会取代vue2.x的data()函数,返回一个对象,暴露给模板,而且只在初始化的时候调用一次,因为值可以被跟踪,所以我们通过vue3来改变编程习惯

首先引入ref

使用数据需要 return

```js
import {ref} from 'vue'

setup() {
  const msg = ref('王大合')
  const age = ref(18)
  function add() {
    age.value +=1
  }
  return {msg,age,add}
}
```

**computed**

```
<template>
<div id="app">
  <img alt="Vue logo" src="./assets/logo.png">
  <div>{{msg}}的年龄为{{age}}</div>
  <div>{{double}}</div>
  <button @click="add">+</button>
</div>
</template>

<script>
import {computed, ref} from 'vue'

export default {

name: 'App',
setup() {
  const msg = ref('王大合')
  const age = ref(18)
  const double = computed(() =>{
    return age.value * 2
  })
  function add() {
    age.value += 1
  }
  return {msg,age,add,double}
   
}
}
</script>
```



##### reactive

在 `setup` 函数里面， 我们适应了 Vue3.0 的第一个新接口 `reactive` 它主要是处理你的对象让它经过 `Proxy` 的加工变为一个响应式的对象，



##### toRefs

用于将响应式对象变成普通对象

```
<template>
<div id="app">
  <img alt="Vue logo" src="./assets/logo.png">
  <div>{{msg}}的年龄为{{age}}</div>
  <div>{{double}}</div>
  <button @click="add">+</button>
</div>
</template>

<script>
import {computed, reactive,toRefs} from 'vue'

export default {

name: 'App',
setup() {
  const state = reactive({
      msg:'王大合',
      age:18,
      double : computed(() =>{
    return state.age * 2
  })
  })

  function add() {
    state.age += 1
  }
  return {...toRefs(state),add}
   
}
}
</script>
```

##### props 和 context

在 `Vue2.0` 中我们可以使用 `props` 属性值完成父子通信，在这里我们需要定义 `props` 属性去定义接受值的类型，然后我们可以利用 `setup` 的第一个参数获取 `props` 使用。

```
export default {

name: 'App',
components:{
  Content
},
setup() {
  const state = reactive({
      msg:'王大合',
      age:18,
      double : computed(() =>{
    return state.age * 2
  })
  })

  function add() {
    state.age += 1
  }
  return {...toRefs(state),add}
   
}
}
```

我们在 `App.vue` 里面就可以使用该头部组件，有了上面的 `props` 我们可以根据传进来的值，让这个头部组件呈现不同的状态。

```
<template>
<div id="app">
  <img alt="Vue logo" src="./assets/logo.png">
  <div>{{msg}}的年龄为{{age}}</div>
  <div>{{double}}</div>
  <Content :msg='msg' />
  <button @click="add">+</button>
</div>
</template>
```

这里我新建一个新的组件content,在app.vue中引入

```
<!-- -->
<template>
<div>{{data}}</div>
</template>

<script>
import {ref} from 'vue'
export default {
name:'content',
props:{
    msg:String
},
setup(props) {
    const data = ref(props.msg)
    return {data}
}
}

</script>
```

`setup` 函数的第二个参数是一个上下文对象，这个上下文对象中包含了一些有用的属性，这些属性在 `Vue2.0` 中需要通过 `this` 才能访问到，在 `vue3.0` 中，访问他们变成以下形式：

```
setup(props, ctx) {
console.log(ctx) // 在 setup() 函数中无法访问到 this
console.log(this) // undefined
}
```

具体能访问到以下有用的属性：

```
- slot
- attrs
- emit
```



父组件

```
<template>
<div id="app">
  <img alt="Vue logo" src="./assets/logo.png">
  <div>{{msg}}的年龄为{{age}}</div>
  <div>{{double}}</div>
  <Content :msg='msg' @change='showName' />
  <button @click="add">+</button>
</div>
</template>

<script>
import {computed, reactive,toRefs} from 'vue'
import Content from './components/content.vue'
export default {

name: 'App',
components:{
  Content
},
 
setup() {
  const state = reactive({
      msg:'王大合',
      age:18,
      double : computed(() =>{
        return state.age * 2
      })
  })
  function showName(params) {
      alert(params)
  }

  function add() {
    state.age += 1
  }
  return {...toRefs(state),add,showName}
   
}
}
</script>
```

子组件

```
<!-- -->
<template>
<div>{{data}}</div>
<button @click="changeName">打个招呼!</button>
</template>

<script>
import {ref} from 'vue'
export default {
name:'content',
props:{
    msg:String
},
setup(props,context) {
    const data = ref(props.msg)
  function changeName() {
      context.emit('change','Hello,王大合!')
  }
    return {data,changeName}
}
}

</script>
```

##### watch

监听ref

不指定数据源

```
const a = ref(18)

watch(()=>{
console.log(a.value)
})
```

指定数据源

```
const a = ref(18)

watch(a,()=> {

  console.log(a.value)

})
```

监听reactive

```
const state = reactive({
      msg:'王大合',
      age:18,
      double : computed(() =>{
        return state.age * 2
      })
  })
```

不指定数据源

```
watch(()=>{
console.log(state.age)
})
```

指定数据源

```
watch(()=>state.age,()=>{
console.log(state.age)
})
```

回调函数参数以及watche clean,使用clean时候是处理重复性的watch监听事件

```
watch(() => state.age,(newVal,oldVal,clean)=> {
    console.log(state.msg + "去年年纪:"+oldVal +"今年年纪:" + newVal)
    clean(
      ()=>{
        console.log('clean')
      }
    )
  })
```

## vue3.X+vite+typescript

##### 放弃webpack,使用vite安装vue3.0

这个是尤大开发的新工具，目的是以后替代webpack，原理是利用浏览器现在已经支持es6的import了，遇到import会发送一个http请求去加载文件，vite拦截这些请求，做一些预编译，省去了webpack冗长打包的时间，提升开发体验

```
npm install -g create-vite-app
create-vite-app vue3-vite
cd vue3-vite
npm install
npm run dev
# 或者使用yarn
yarn add -g create-vite-app
yarn create vite-app <project-name>
```

安装依赖

```
yarn
```

使用yarn启动项目

```
yarn dev
```



##### 引入typescript

```
# 安装 typescript

yarn add typescript -D
```

初始化`tsconfig.json`

```
# 然后在控制台执行下面命令
npx tsc --init
```

将`main.js`修改为`main.ts`,同时将`index.html`里面的引用也修改为`main.ts`,

然后在script 里添加 lang="ts"

```
<template>
<img alt="Vue logo" src="./assets/logo.png" />
<HelloWorld msg="Hello Vue 3.0 + Vite" />
</template>

<script lang="ts">
import HelloWorld from './components/HelloWorld.vue'

export default {
name: 'App',
components: {
  HelloWorld
}
}
</script>
```

修改完之后，重启就可以访问项目了。虽然这样配置是可以了，但是打开`main.ts`会发现`import App from App.vue`会报错:`Cannot find module './App.vue' or its corresponding type declarations.`,这是因为现在`ts`还没有识别`vue`文件，需要进行下面的配置:

在项目根目录添加`shim.d.ts`文件

```
# powerShell终端,也可以手动创建
New-Item shim.d.ts
```

添加以下内容

```
declare module "*.vue" {
import { Component } from "vue";
const component: Component;
export default component;
}
```



##### 安装vue-router

```
yarn add vue-router@4.0
```

这样可以选择最新的vue-router 4.0.0的测试版本,这里更新到beta.13

##### 配置vue-router

在项目`src`目录下面新建`router`目录，然后添加`index.ts`文件，在文件中添加以下内容

```
import {createRouter, createWebHashHistory} from 'vue-router'

// 在 Vue-router新版本中，需要使用createRouter来创建路由
export default createRouter({
// 指定路由的模式,此处使用的是hash模式
history: createWebHashHistory(),
// 路由地址
routes: []
})
```

##### 安装vuex

同上

```
yarn add vuex@4.0
```

目前只能选择最新测试版

在项目`src`目录下面新建`store`目录，并添加`index.ts`文件，文件中添加以下内容

```
import { createStore } from 'vuex'

interface State {
userName: string
}

export default createStore({
state:{
userName:'王大合'
}
});
```

main.ts中引入vuex和vue-router

```
import { createApp } from 'vue'
import App from './App.vue'
import './index.css'
import router from './router/index'
import vuex from './store/index'

const app = createApp(App)

app.use(router)
app.use(vuex)
app.mount('#app')
```

## typescript+vue入门

### 原始数据类型

JavaScript 的类型分为两种：原始数据类型（Primitive data types）和对象类型（Object types）。

原始数据类型包括：布尔值、数值、字符串、`null`、`undefined` 以及 ES6 中的新类型 `Symbol`。

本节主要介绍**前五种**原始数据类型在 TypeScript 中的应用。

##### 布尔值§

布尔值是最基础的数据类型，在 TypeScript 中，使用 `boolean` 定义布尔值类型：

```
let isDone: boolean = false;

// 编译通过
// 后面约定，未强调编译错误的代码片段，默认为编译通过
```

注意，使用构造函数 `Boolean` 创造的对象**不是**布尔值：

```
let createdByNewBoolean: boolean = new Boolean(1);

// Type 'Boolean' is not assignable to type 'boolean'.
//   'boolean' is a primitive, but 'Boolean' is a wrapper object. Prefer using 'boolean' when possible.
```

事实上 `new Boolean()` 返回的是一个 `Boolean` 对象：

```
let createdByNewBoolean: Boolean = new Boolean(1);
```

直接调用 `Boolean` 也可以返回一个 `boolean` 类型：

```
let createdByBoolean: boolean = Boolean(1);
```

在 TypeScript 中，`boolean` 是 JavaScript 中的基本类型，而 `Boolean` 是 JavaScript 中的构造函数。其他基本类型（除了 `null` 和 `undefined`）一样，不再赘述。

##### 数值§

使用 `number` 定义数值类型：

```
let decLiteral: number = 6;
let hexLiteral: number = 0xf00d;
// ES6 中的二进制表示法
let binaryLiteral: number = 0b1010;
// ES6 中的八进制表示法
let octalLiteral: number = 0o744;
let notANumber: number = NaN;
let infinityNumber: number = Infinity;
```

编译结果：

```
var decLiteral = 6;
var hexLiteral = 0xf00d;
// ES6 中的二进制表示法
var binaryLiteral = 10;
// ES6 中的八进制表示法
var octalLiteral = 484;
var notANumber = NaN;
var infinityNumber = Infinity;
```

其中 `0b1010` 和 `0o744` 是 ES6 中的二进制和八进制表示法，它们会被编译为十进制数字。

##### 字符串§

使用 `string` 定义字符串类型：

```
let myName: string = 'Tom';
let myAge: number = 25;

// 模板字符串
let sentence: string = `Hello, my name is ${myName}.
I'll be ${myAge + 1} years old next month.`;
```

编译结果：

```
var myName = 'Tom';
var myAge = 25;
// 模板字符串
var sentence = "Hello, my name is " + myName + ".
I'll be " + (myAge + 1) + " years old next month.";
```

其中 ``` 用来定义 [ES6 中的模板字符串](http://es6.ruanyifeng.com/#docs/string#模板字符串)，`${expr}` 用来在模板字符串中嵌入表达式。

##### 空值§

JavaScript 没有空值（Void）的概念，在 TypeScript 中，可以用 `void` 表示没有任何返回值的函数：

```
function alertName(): void {
   alert('My name is Tom');
}
```

声明一个 `void` 类型的变量没有什么用，因为你只能将它赋值为 `undefined` 和 `null`：

```
let unusable: void = undefined;
```

##### Null 和 Undefined[§](https://ts.xcatliu.com/basics/primitive-data-types.html#null-和-undefined

在 TypeScript 中，可以使用 `null` 和 `undefined` 来定义这两个原始数据类型：

```
let u: undefined = undefined;
let n: null = null;
```

与 `void` 的区别是，`undefined` 和 `null` 是所有类型的子类型。也就是说 `undefined` 类型的变量，可以赋值给 `number` 类型的变量：

```
// 这样不会报错
let num: number = undefined;
// 这样也不会报错
let u: undefined;
let num: number = u;
```

而 `void` 类型的变量不能赋值给 `number` 类型的变量：

```
let u: void;
let num: number = u;

// Type 'void' is not assignable to type 'number'.
```

## 上线小项目todoList

##### app.vue

```
<template>
<div id="app">
  <div id="nav">
    <router-link to="/">todoList</router-link> | 
    <router-link to="/about">About</router-link>
  </div>
  <router-view/>
</div>
</template>

<script lang="ts">

export default {
name: 'App'
}
</script>

<style lang="scss">
#app {
font-family: Avenir, Helvetica, Arial, sans-serif;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
text-align: center;
color: #2c3e50;
}

#nav {
padding: 30px;

a {
  font-weight: bold;
  color: #2c3e50;

  &.router-link-exact-active {
    color: #42b983;
  }
}
}
</style>
```

##### 配置路由 router/index.ts

```
import {createRouter, createWebHashHistory} from 'vue-router'

// 在 Vue-router新版本中，需要使用createRouter来创建路由
export default createRouter({
// 指定路由的模式,此处使用的是hash模式
history: createWebHashHistory(),
// 路由地址
routes: [
  {
  path: '/',
  // 必须添加.vue后缀
  component: () => import('../views/todo-list.vue')
    },
  {
      path: '/about',
      name: 'About',
      
      component: () => import('../views/About.vue')
    }
]
})
```

##### store的index.ts新建vuex

```
import { createStore } from 'vuex'

interface State {
userName: string
taskList: any[]
 
}

export default createStore({
state: {
   
    userName: "王大合",
    taskList: []
     
},
mutations:{
   
  createTask (state:any, newTask:string) {
      state.taskList.push(newTask)
    },
    deleteTask (state:any, index:number) {
      state.taskList.splice(index, 1)
    },
    updateStatus (state:any, payload:any) {
      const { index, status } = payload
 
      state.taskList[index].isfinished = status
    }
}
});
```

##### 在src目录新建view文件夹,创建todoList和about

todoList

```
<template>
<div class="home">
  <!-- input输入list内容 -->
  <div>
      <input
  @keyup.enter="addTask"
    class="input"
    type="text"
    v-model="inputValue"
    placeholder="请输入" />
  </div>
  <!-- todoList内容展示和删除 -->
    <ul class="ul">
    <li class="item" v-for="(item, index) in taskList" :key="index">
      <p
      @click="updateStatus(index, !item.isfinished)"
      class="content"
      :class="item.isfinished ? 'active' : ''"
      >{{item.lable}}</p>
      <div class="item-delete" @click="deleteTask(index)">X</div>
    </li>
    <li v-if="taskList.length === 0" class="item-none">暂无数据</li>
  </ul>
</div>
</template>


<script lang="ts">

import { ref, computed } from 'vue';
import { useStore } from "vuex";
export default {
 
setup() {
  const store = useStore()
  const taskList = computed(() => store.state.taskList);
  const inputValue = ref('');
  const addTask = () => {
    store.commit('createTask', {
      lable: inputValue.value,
      isfinished: false
    })

    inputValue.value = ''
  }

  const updateStatus = (index, status) => {
    store.commit('updateStatus', {
      index,
      status
    })
  }

  const deleteTask = (index) => {
    store.commit('deleteTask', index)
  }

  return {
    inputValue,
    taskList,
    addTask,
    updateStatus,
    deleteTask
  };
}
}
</script>

<style scoped lang='scss'>
* {
box-sizing: border-box;
margin: 0;
padding: 0;
}
ul,
li {
list-style: none;

text-align: left;
}
.home {
max-width: 400px;
margin: 0 auto;
.input {
  width: 100%;
  height: 40px;
  border-radius: 5px;
  outline-style: none;
  border: 2px solid #999;
  padding: 5px 10px;
}
.ul {
  margin-top: 10px;
}

.item {
  height: 40px;
  line-height: 40px;
  padding-bottom: 5px;
  border-bottom: 1px solid #dcdfe6;
  color: #333333;
}
.item-none {
  height: 40px;
  line-height: 40px;
  padding-bottom: 5px;
  color: #333333;
  text-align: center;
}
.content {
  float: left;
  height: 40px;
  line-height: 40px;
  cursor: pointer;
}
p.active {
  text-decoration:line-through; 
  color: #999999;
}
.item-delete {
  float: right;
  width: 25px;
  text-align: center;
  cursor: pointer;
}
}
</style>
```

about

```
<template>
<div class="about">
  <h1>{{name}}</h1>
   

   
</div>
</template>

<script lang='ts'>
import { ref, watch } from 'vue';

export default {
name: 'about',
setup() {
  const name = ref('王大合出品');

  
   
  return {
    name,
    
  };
}
};
</script>
```



