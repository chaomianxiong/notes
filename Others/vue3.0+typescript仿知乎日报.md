## vue3.0+typescript仿知乎日报

王大合 [王大合](javascript:void(0);) *2020-12-16*

```
title: vue3.0+typescript仿知乎日报
date: 2020-10-28 16:05:55
tags:
categories: vue
```

# vue3.0+typescript仿知乎日报

## 创建项目以及安装依赖

##### 使用vite创建项目

```
# 或者使用yarn
yarn add -g create-vite-app
yarn create vite-app <project-name>
#yarn初始化packeage依赖,并且运行
yarn 
yarn dev
```

安装依赖

我需要使用

| 依赖库包   |
| ---------- |
| typescript |
| vuex       |
| vue-router |
| sass       |

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

安装 sass  sass-loader

```
yarn add sass sass-loader -D
```



## vite配置

在项目中创建一个`vite.config.js`或`vite.config.ts`文件。如果在当前工作目录中找到Vite，它将自动使用它。

官网 config.ts配置参考:https://github.com/vitejs/vite/blob/master/src/node/config.ts

```
New-Item vite.config.ts
```

配置vite

```
import type { UserConfig } from 'vite';



const viteConfig: UserConfig = {
  /* 端口号 */
  port:3555,

  /* hostname */
  hostname: 'localhost',

  /* 运行自动打开浏览器 */
  open:false,

  
   
};

export default viteConfig;
```

新建api文件夹

引入axios

```
yarn add axios -S
```

在api文件夹创建axios.ts引入axios,并且把axios baseURL设置为: '/api',解决跨域

```
import axios from 'axios'

const request = axios.create({
baseURL: '/api'
})

export default request
```

跨域解决了,外部接口就可以使用了,我使用的是unicloud的云函数url

在api文件夹,新建index.ts,可以写后端接口了

```
import request from './axios'

// 获取首页新闻数据
export const getNewsList = ()=>{
return request({
url:'/newsList'
})
}
```





## 首页Header组件

在src目录创建vue文件夹,新建index.vue,

app.vue清理多余代码,引入<router-view />;

并且删除helloword

```
<template>
<router-view />
</template>

<script lang="ts">


export default {
name: 'App',
 
}
</script>
```

在components创建Header.vue

```
<template>
<header class="headerBox">
  <div class="title">
    <div class="time">
      <span>{{day}}日</span>
      <span>{{month}}月</span>
    </div>
    <h1>知乎日报</h1>
  </div>
  <div class="pic">
    <img />
  </div>
</header>
</template>
<script lang="ts">
export default {
props:{
  day: {
    type: String,
    default: '-'
  },
  month: {
    type: String,
    default: '-'
  }
}
};
</script>
<style lang="scss" scoped>
.headerBox {
width: 100%;;
display: flex;
justify-content: space-between;
align-items: center;
position: fixed;
top: 0;
left: 0;
.title {
  display: flex;
   
  flex-wrap: nowrap;
  align-items: center;
  .time {
    display: flex;
    flex-direction: column;
    padding: 0 1rem;
    border-right: 0.2rem solid #eee;
    span {
      display: block;
      text-align: center;
      font-size: 1.5rem;
      &:nth-child(1) {
        font-size: 2rem;
        font-weight: bold;
      }
    }
  }
  h1 {
    padding: 0 1rem;
  }
}
.pic {
  width: 3rem;
  height: 3rem;
  margin-right: 3rem;
  background: url("../assets/images/timg.jpg") no-repeat;
  background-size: 100% 100%;
  border-radius: 50%;

  img {
    display: block;
    width: 100%;
    height: 100%;
  }
}

}

</style>
```

新建utils文件夹，创建index.ts

拆分时间日期formatTime

```
function formatTime(time:any) {
  let arr:any[] = [];
  time = time.toLocaleDateString();
  time.replace(/\d+/g, (val:any) => {
    val = val < 2 ? `0${val}` : val;
    arr.push(val);
  });
  return arr;
}

export default {
  formatTime
};
```

前端引入utils,并且把时间month和day数据传给子组件

```
<!-- -->
<template>
<div class="home">
    <zhihuHeader :day="day" :month="month" />
</div>
</template>

<script lang="ts">
import zhihuHeader from '../components/Header.vue'
import {reactive,toRefs,computed} from 'vue'
import utils from "../utils";

export default {
  components:{
      zhihuHeader
  },

  setup() {
      const state = reactive({
          date:new Date(),
      })
       
      let day = computed(()=> utils.formatTime(state.date)[2])
      let month = computed(() => utils.formatTime(state.date)[1]);
      return {
          ...toRefs(state),
          day,
          month 
      }
      console.log(day)
  }

};


</script>


<style lang='scss' scoped>
.home {
  widows: 100%;
  height: 100%;
}
</style>
```





vite使用proxy代理解决跨域

同源策略

协议相同 http https

域名相同 www.XXX

端口号相同 www.XXX:80

proxy代理

cors

nginx

```
import type { UserConfig } from 'vite';



const viteConfig: UserConfig = {
  /* 端口号 */
  port:3555,

  /* hostname */
  hostname: 'localhost',

  /* 运行自动打开浏览器 */
  open:false,

  /* proxy */
  
      proxy: {
               
              '/api': {
              target: 'https://uni937d4b0-6cc760.service.tcloudbase.com',
              changeOrigin: true,
              rewrite: path => path.replace(/^\/api/, '')
          }
      }
   
};

export default viteConfig;
```

## 使用axios并且配置proxy代理跨域

在vite.config.ts添加proxy

```
import type { UserConfig } from 'vite';
const path = require('path')


const viteConfig: UserConfig = {
  /* 端口号 */
  port:3555,

  /* hostname */
  hostname: 'localhost',

  /* 运行自动打开浏览器 */
  open:false,

  alias: {
      '/@/': path.resolve(__dirname, './src'),
      '/@views/': path.resolve(__dirname, './src/views'),
      '/@components/': path.resolve(__dirname, './src/components'),
      '/@utils/': path.resolve(__dirname, './src/utils'),
    },
  /* proxy */
  
      proxy: {
               
              '/api': {
              target: 'https://uni937d4b0-6cc760.service.tcloudbase.com',
              changeOrigin: true,
              ws:true,
              rewrite: path => path.replace(/^\/api/, '')
          }
      }
   
};

export default viteConfig;
```

引入axios

```
yarn add axios -S
```



在src目录下创建api文件夹封装axios接口

创建axios.ts和index.ts



axios.ts

```
import axios from 'axios';


var instance = axios.create({
baseURL: 'http://localhost:3555/api/'
 
});





export default instance;
```

index.ts

```
import instance from './axios'

// 获取首页新闻数据
export const getBannerList = () =>{
return instance({
url:'/bannerList'
})
}

export default {
getBannerList
}
```

在首页index.vue中引入axios封装好的api接口

然后置入onbeforeMount当中

了解下vue3.0生命周期

```
被替换

beforeCreate -> setup()
created -> setup()

重命名

beforeMount -> onBeforeMount
mounted -> onMounted
beforeUpdate -> onBeforeUpdate
updated -> onUpdated
beforeDestroy -> onBeforeUnmount
destroyed -> onUnmounted
errorCaptured -> onErrorCaptured
```

index.vue当中引入getBannnerList

```
<!-- -->
<template>
<div class="home">
    <zhihuHeader :day="day" :month="month" />
    <zhihu-banner :bannerData="bannerData" />
     
     
</div>
</template>

<script lang="ts">
import zhihuHeader from '../components/Header.vue'
import zhihuBanner from '/@/components/Banner.vue';
import {reactive,toRefs,computed, onBeforeMount} from 'vue'
import {getBannerList} from '../api/index'
import utils from "../utils";

export default {
  components:{
      zhihuHeader,
      zhihuBanner
  },

  setup() {
      const state = reactive({
          date:new Date(),
          bannerData: [],
          
      })
       
      let day = computed(()=> utils.formatTime(state.date)[2])
      let month = computed(() => utils.formatTime(state.date)[1]);

const getBannerData = async () => {
    const res = await getBannerList()
    state.bannerData = res.data.data
    console.log(state.bannerData)
        }
        
      onBeforeMount(() => {
          getBannerData()
      })

      return {
          ...toRefs(state),
          day,
          month 
      }
     
  }

};


</script>


<style lang='scss' scoped>
.home {
  widows: 100%;
  height: 100%;
}
</style>
```



## 使用mockjs模拟数据

首先安装mockjs 

```
yarn add mockjs -S
```

在src目录下新建api文件夹

创建mockjs.ts,并且引入 mockjs 

```
import Mock from 'mockjs'
```

因为ts无法识别到mockjs，所以在shim.d.ts末尾处添加

```
declare module 'mockjs'
```

在mockjs当中加上bannerList

```
Mock.mock('/api/bannerList','get',{ "data": [
  {
      "id": "1",
      "img": "https://pic4.zhimg.com/v2-f05c0e1005121e89e53762704d05b28c_fhd.jpg?source=8673f162",
      "title": "金发碧眼为什么很少在白人以外的种族出现？"
    },
    {
      "id": "2",
      "img": "https://pic2.zhimg.com/v2-86bcc639835a991b61602b73310604b8_fhd.jpg?source=8673f162",
      "title": "《哈利波特》原著中与电影中人物有哪些差别？"
    },
    {
      "id": "3",
      "title": "有哪些适合情侣两个人一起玩的桌游？",
      "img": "https://pic1.zhimg.com/v2-89f0e1611118a7e15694060542eeba7a_fhd.jpg?source=8673f162"
    }
]})
```

main.ts引入mockjs

```
imoport './api/mock'
```

axios.ts配置baseURl为'/api/'即可调用mock数据



## vant UI框架 生成banner轮播图

首先安装配置下vant 

目前安装vant3需要使用命令

```
yarn add vant@next -S
```

main.ts导入

```
import Vant from 'vant';
import 'vant/lib/index.css';
```

在components中新建Banner.vue组件

引用vant的 swipe-view

```
<!-- banner -->
<template>
<div class="swipe-content">
  <van-swipe class="my-swipe" :autoplay="3000" :show-indicators=false>
      <van-swipe-item class="van-swipe-item" v-for="(item,index) in bannerData" :key="index">
          <img :src="item.img" >
          <h5 style="position:absolute; bottom:2rem; left:2rem;">{{item.title}}</h5>
      </van-swipe-item>
  </van-swipe>
</div>
</template>

<script>
export default {
props: {
  bannerData: {
    type: Array,
  },
},
};
</script>
<style lang='scss' scoped>
.swipe-content {
margin-top:6rem;
}

.my-swipe .van-swipe-item {
  color: #fff;
  font-size: 1rem;
  line-height: 6rem;
  text-align: center;
  background-color: #fff;
  img {
      width:100%;
      height:30rem;
  }
}
</style>
```

在首页引入组件即可

```
import zhihuBanner from '../components/Banner.vue'
```

传值给子组件

```
<zhihu-banner :bannerData="bannerData" />
```



## 新闻列表组件开发

先mock新闻列表数据

```
Mock.mock('/api/newsList','get',{
  "data": [
      {
        "id": "1",
        "images": [
          "https://pic4.zhimg.com/v2-f05c0e1005121e89e53762704d05b28c_fhd.jpg?source=8673f162",

        ],
        "title": "金发碧眼为什么很少在白人以外的种族出现？",
        "author": "作者 / biokiwi"
      },
      {
        "id": "2",
        "title": "《哈利波特》原著中与电影中人物有哪些差别？",
        "author": "作者 / kalinnn",
        "images": [
          "https://pic2.zhimg.com/v2-86bcc639835a991b61602b73310604b8_fhd.jpg?source=8673f162"
        ]
      },
      {
        "id": "3",
        "title": "有哪些适合情侣两个人一起玩的桌游？",
        "author": "作者 / 北邙",
        "images": [
          "https://pic1.zhimg.com/v2-89f0e1611118a7e15694060542eeba7a_fhd.jpg?source=8673f162"
        ]
      }
    ]
})
```

在axios中配置数据输出

```
// 获取首页newsList数据
export const getNewsList = () =>{
return instance({
url:'/newsList'
})
}
```



同样在components中新建NewsItem.vue

```
<template>
<div>
  <div v-for="item in news" :key="item.id">
    <router-link :to="{path:`/detail/${item.id}`}" class="newsItem">
      <div class="con">
        <h4>{{item.title}}</h4>
        <span>{{item.author}}</span>
      </div>
      <div class="pic">
        <img :src="item.images[0]" alt />
      </div>
    </router-link>
  </div>
</div>
</template>
<script>
export default {
  props: {
  news: {
    type: Array
  }
},
 
};
</script>
<style lang="scss">
.newsItem {
display: flex;
justify-content: space-between;
align-items: center;
padding: 0.5rem 0;
margin:0 0.5rem;
border-bottom:0.1rem solid #eee;
.con {
  display: flex;
  flex-direction: column;
  margin-right: 0.3rem;
  color: #000;

  h4 {
      float: left;
      width:15rem;
      text-overflow:ellipsis;
      white-space:nowrap;
      margin: 1rem 1rem;
    font-size: 1rem;
    font-weight: normal;
    line-height: 1rem;
    overflow: hidden;
  }

  span {
    display:flex;
    justify-content: flex-start;
    color: #999;
    line-height: 0.5rem;
    margin: 0 1rem;
  }
}
.pic {
  width: 6rem;
  height: 4rem;
  background: #eee;
  margin-right:0.5rem;
  img {
    display: block;
    width: 100%;
    height: 100%;
    border-radius: 0.1rem;
  }
}
}
</style>
```

在index引入



```
import zhihuNewsItem from '../components/NewsItem.vue'
```

传递数据给子组件



```
<zhihu-newsItem :news="newsData" />
```





## 详情页开发

首先mock下数据，这次需要传参

```
Mock.mock(('/api/detailList'),'post',(options:any) => {
  let {id} = JSON.parse(options.body)
  console.log(id)

if(id == 1) {
      let data = {
        "author": "作者 / biokiwi",
        "body":"<div > \n <p><strong><strong>是什么决定了眼色和发色？</strong></strong></p> \n <p>探究题主的问题之前，我们应该先了解一下眼色、发色的形成机制。其实眼睛和头发的颜色类似于皮肤，都是由于<strong>不同的色素沉淀</strong>导致的结果，只是可能因为其中涉及的色素差异，会有些许不同。</p>\n <p>眼睛色彩相对简单，主要就是<strong>黑色素</strong>沉淀的多少，决定了你眼睛是什么颜色。眼睛的结构图相信不少人都有看过，从正面看的话，中间最黑的地方就是瞳孔，而有颜色的一圈则是虹膜，虹膜内的黑色素细胞就决定了眼睛颜色。</p> \n <img  src=\"https://pic1.zhimg.com/v2-3ec9c9111d760b6b59f622a5ef3ee02a_720w.jpg?source=8673f162\"> \n <p>细胞中会含有一种叫<strong>黑色素体</strong>的细胞器。不同的人细胞里黑色体是不一样的，进而改变了虹膜的吸收光线的能力，眼睛也会呈现出不一样的颜色：黑素体少，呈现半透明的虹膜就会因为丁达尔效应反射出蓝色或者绿色的眼睛，而黑色素体较多，虹膜吸光能力也更强，就会呈现出深褐色的眼睛。</p> </div>",
        "id": 1,
        "img": "https://pic4.zhimg.com/v2-f05c0e1005121e89e53762704d05b28c_fhd.jpg?source=8673f162",
        "time": "2小时前",
        "title": "金发碧眼为什么很少在白人以外的种族出现？"
      }

      return data
       
  } else if(id == 2) {
    let data = {
       
        "author": "作者 / kalinnn",
        "body": "<div class=\"main-wrap content-wrap\">\n <p>我很满意鲁伯特塑造的罗恩，他在里面同龄人中演技可以说数一数二，非常自然。就像罗琳说的，「他是个天才，不用我多说，他好像天生就知道怎么演好罗恩。」</p> \n <p>罗恩没有电影里那么傻憨，电影里的罗恩被弱化太多太多了。</p> \n <p>但我不满意编剧导演塑造的罗恩。</p> \n <p>电影这里的改编应该是为了弥补后面删掉了赫敏逻辑推理出毒药魔药的高光片段，好让赫敏在最后学院杯中得分。所以只能把罗恩搞弱，把赫敏高光移到魔鬼网这里。</p> \n <p>电影这里的改编应该是为了弥补后面删掉了赫敏逻辑推理出毒药魔药的高光片段，好让赫敏在最后学院杯中得分。所以只能把罗恩搞弱，把赫敏高光移到魔鬼网这里。</p> </div>",
        "id": 2,
        "img": "https://pic2.zhimg.com/v2-86bcc639835a991b61602b73310604b8_fhd.jpg?source=8673f162",
        "time": "30分钟前",
        "title": "《哈利波特》原著中与电影中人物有哪些差别？"
       
       
    }

    return data
  } else if(id == 3) {
    let data = {
      "author": "作者 / 北邙",
      "body": "<div > \n <p>（以下为一些个人废话感想，只想了解桌游的朋友可以直接拉下）</p> \n <p>【我自己是属于桌游的收藏爱好者，这两年来陆陆续续入着，前几天一清算，连上各种系列的大小扩和循环，以及 larp 的剧本，家里的藏品已经破了 180 种，稳稳地往着 200 大关去了。</p> \n <p>今年来能感觉得到，国内桌游市场逐渐火了起来，越来越多的人开始涉及了解这个圈子，身边的朋友也大多开始对这些感兴趣了，聚会的时候不再只是抱着手机打王者，或者清一色的狼人三国杀，而是会提前请我带一些桌游去，或者干脆来我家随便玩。作为一个专业推新的半硬核老玩家，这一点让我非常非常得欣慰。</p> \n <p>今年来能感觉得到，国内桌游市场逐渐火了起来，越来越多的人开始涉及了解这个圈子，身边的朋友也大多开始对这些感兴趣了，聚会的时候不再只是抱着手机打王者，或者清一色的狼人三国杀，而是会提前请我带一些桌游去，或者干脆来我家随便玩。作为一个专业推新的半硬核老玩家，这一点让我非常非常得欣慰。</p> </div>",
      "id": 3,
      "img": "https://pic1.zhimg.com/v2-89f0e1611118a7e15694060542eeba7a_fhd.jpg?source=8673f162",
      "time": "2小时前",
      "title": "有哪些适合情侣两个人一起玩的桌游？"
    }

    return data
  }
   
})
```

在api文件的index.ts中添加

```
//获取newsDetail数据
export const getNewsDetail = (id:any) => {
return instance.post('/detailList',{
id
})
}
```

首先在路由中添加detail

```
import DETAIL from '../views/detail.vue'
```

routes中添加

```
{
    path:'/detail/:id',
    name:"详情",
    component:DETAIL
  }
```

然后开发detail详情

```
<!-- -->
<template>
<div class="detailBox">

  <!-- nav -->
<van-nav-bar left-text="返回" 
left-arrow  
@click-left="$router.push('/')"
@click-right="showShare = true">
  <template #right>
    <van-icon name="arrow" size="18" />
  </template>
</van-nav-bar>
  <!-- 分享面板 -->
      <van-share-sheet
        v-model:show="showShare"
        title="立即分享给好友"
        :options="options"
        
      />
  <!-- 文章内容 -->
      
  <div class="headBox">
      <h3>{{title}}</h3>
      <span>{{ author }}</span>
  </div>
     
  <div class="content" v-html="body"></div>
  <!-- 结尾button -->
   
  <van-button type="primary">进入[知乎]查看相关讨论</van-button>
</div>
</template>

<script>
import {reactive,toRefs,watch,ref,onMounted} from 'vue'
import {getNewsDetail} from '../api/index'

export default {
setup() {
   
  let id = ref(0);
  const state = reactive({
    showShare: false,
    options: [
      { name: '微信', icon: 'wechat' },
      { name: '微博', icon: 'weibo' },
      { name: '复制链接', icon: 'link' },
      { name: '分享海报', icon: 'poster' },
      { name: '二维码', icon: 'qrcode' },
    ],
    title:'',
    author:'',
    body:''
  })

  watch(id,async() => {
    const res = await getNewsDetail(id.value)
    let {title, author, body} = res.data
    console.log(res.data)
    state.title = title
    state.author = author
    state.body = body
  })


  return {
    id,
    ...toRefs(state)
  }
},

 
    beforeMount(){
  let { id } = this.$route.params
  this.id = id
   
}
}

</script>
<style lang='scss' scoped>
.detailBox {
    display: flex;
    width: 100%;
    height: 100%;
    flex-direction: column;
    padding:0 0.5rem;
  .headBox {
     
    box-sizing: border-box;
    padding: 0.2rem;
    width: 100%;
    background: linear-gradient(
      0,
      rgba(55, 86, 103, 0.5),
      rgba(55, 86, 103, 0)
    );
    color: #fff;
    line-height: 1.4rem;

    h3 {
      font-size: 1rem;
    }

    span {
      display: block;
      font-size: 0.4rem;
      text-align: right;
    }
  }
}
</style>
```





阅读 2