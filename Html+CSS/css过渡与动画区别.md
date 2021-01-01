作者：前端天宇
链接：https://zhuanlan.zhihu.com/p/145929287
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



**css过渡和动画的区别：**

animation属性类似于transition，他们都是随着时间改变元素的属性值，那么区别是什么？

其主要区别在于：transition需要触发一个事件才会随着时间改变其CSS属性；animation在不需要触发任何事件的情况下，也可以显式的随时间变化来改变元素CSS属性，达到一种动画的效果。

1）动画不需要事件触发，过渡需要。

2）过渡只有一组（两个：开始-结束） 关键帧，动画可以设置多个。

**过渡(transition)**

过渡就是使瞬间的样式变化，按照一定方式变得缓慢平缓；

例如鼠标划过超链接时颜色的变化，点击按钮后的颜色变化等，默认转化都是瞬间完成，可能你已经习惯了这种变换，但有时候平缓一些看着还是比较舒适的；

要实现样式的过渡变化，那么首先就学要有样式变换，例如鼠标划过，单击按钮，点击图片等操作，来实现颜色，尺寸，位置等样式的变化；

下面是鼠标划过段落使文本变红的操作，应用所有 **transition**属性：

```text
p:hover {
    color: red;
}
p {
    transition-property: color;
    transition-duration: 2s;
    transition-timing-function: linear;
    transition-delay: 0;
}
```

一共四个值，功能基本都是字面翻译的意思：

**transition-property**

执行过渡的属性，例子设置为颜色color的变化，也可以是width, font-size等，不设置的话默认是all，即所有属性；

**transition-duration**

过渡的时间，单位是秒，如1s, 2.3s，不设置的话默认 0s，即无过渡效果；

**transition-timing-function**

设置过渡时的变化方式，默认是 ease，即速度由慢到快再到慢，常用的还有 linear，线性变化速度均匀，还有其他几个方式，过渡时间短的话看不出什么区别；

**transition-delay**

延迟时间，即多少秒后执行过渡效果，默认 0s，不延迟；

当然这么多单词可能记不住，一般使用快捷写法：

```text
p {
    transition: color 2s linear 0;
}
/*最少要指定过渡时间*/
p {
    transition: 2s;
}
```

也可以设置每个样式分别过渡，例如：

```text
p {
    transition: color 2s linear,
                font-size .5s,
                background: 1s;
}
```

每个样式过渡之间用逗号隔开就行了；

最后，由于是新特性，为了兼容性需要加上浏览器厂商前缀：

```text
p {
    transition: 2s;
    -webkit-transition: 2s;
    -moz-transition: 2s;
    -ms-transition: 2s;
    -o-transition: 2s;
}
```

**动画(animation)**

CSS3的动画是个很不错的技术，基本能取代一些动图，javascript，flash等；

而动画里最重要的概念就是关键帧，也许你用PS做gif动图的时候看见过这个概念，所谓动画就是一帧一帧图片连续切换实现的效果，关键帧就是里面主要的一些帧；

实现CSS动画也需要设置关键帧 @keyframes：

```text
@keyframes my-animation {
    0% {
        color: red;
    }
    50% {
        color: green;
    }
    100% {
        color: blue;
    }
}
```

格式如上，@keyframes后面跟的是自定义的动画名称，后面会用到。里面的0%，50%，100%便是设置的三个关键帧及其对应样式，如果只需要设置首尾两个关键帧，可以这样写：

```text
@keyframes my-animation {
    from {
        color: green;
    }
    to {
        color: blue;
    }
}
```

当然样式除了color还能设置多项样式；

定义好关键帧后就直接在需要应用动画的元素标签内使用就行了，格式及所有属性如下：

```text
p {
    animation-name: my-animation;
    animation-duration: 3s;
    animation-timing-function: ease;
    animation-delay: 0;
    animation-iteration-count: 3;
    animation-direction: normal;
    animation-play-state: running;
}
```

发现了吧，很多属性和transition里面一样，简单介绍下：

- **animation-name**

就是之前跟在@keyframea后面的自定义名称，之前设置的是 my-animation;

- **animation-duration**
- **animation-timing-function**
- **animation-delay**

和前面一样，默认分别为 0, ease, 0；

- **animation-iteration-count**

动画播放的次数，默认 1，但一般设置为 infinite，即无限循环；

- **animation-direction**

动画播放的方向，normal为默认，正向播放，reverse为反向播放，alternate为正向后反向，alternate-reverse为反向后正向；

- **animation-play-state**

播放状态，默认 running，运行，paused为暂停，可以在javascript中使用对动画进行控制；

当然，这个属性比之前的transition还多，也有简便写法：

```text
p {
    animation: my-animation 3s linear infinite alternate;
}
```

其中 animation-name 和 animation-duration为必须设置的属性；

同样，记得考虑浏览器兼容：

```text
@-webkit-keyframes mycanimation {
    from {
        color: green;
    }
    to {
        color: blue;
    }
}
p {
    -webkit-animation: my-animation 3s linear infinite;
}
/* -moz-, -ms-, -o- 格式类似 */
```

**从最零基础开始的的HTML+CSS+JavaScript。jQuery，Ajax，node，angular框架等到移动端HTML5的项目实战【视频＋工具＋系统路线图】都有整理，在线解析，学习指导，点：[【WEB前端学习圈⑤】](https://link.zhihu.com/?target=https%3A//jq.qq.com/%3F_wv%3D1027%26k%3D5G5WpSV)**