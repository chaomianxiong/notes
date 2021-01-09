# vue-cli4.5下antd(ant-design-vue)按需引入配置按需加载

#### 1.创建项目

安装vue-cli(我现在装的是4.3)

```
npm install -g @vue/cli
```

创建项目, 配置可自选，这里我直接回车默认

```
 vue create antd-demo
```

运行，访问 http://localhost:8080/ ，可以看到 Welcome to Your Vue.js App

```
 cd antd-demo
 npm run serve
```

#### 2.引入 ant-design-vue

```
 npm install ant-design-vue -D
```

在main.js中引入Button组件

```javascript
import Vue from 'vue'
import { Button } from 'ant-design-vue'; //引入组件，但不用引入样式
import App from './App.vue'

Vue.component(Button.name, Button); //注册
Vue.config.productionTip = false

new Vue({
  render: h => h(App),
}).$mount('#app')
```

在app.vue里调用Button组件

```html
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
      <a-button type="primary">Button</a-button>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>
```

#### 3.安装babel-plugin-import插件实现按需引入

```
npm install babel-plugin-import --dev
```

将配置文件`babel.config.js`的内容替换为如下

```javascript
module.exports = {
  presets: ["@vue/app"],
  plugins: [
    [
      "import",
      { libraryName: "ant-design-vue", libraryDirectory: "es",
       style: "css" }
    ]
  ]
};
```



```
 npm install less-loader --save-dev
```

```
 npm install less --save-dev
```



`less-loader`配置里开启允许`javascript`

这个方法看起来好点，我用的`vue-cli4`，需要手动在根目录下创建配置文件`vue.config.js`，在`issues`评论里找到对应`vue-cli4`的配置填入。

```javascript
module.exports = {
  css: {
      loaderOptions: {
          less: {
            lessOptions:{
              javascriptEnabled: true,
            }
          }
      }
  },
}
```

