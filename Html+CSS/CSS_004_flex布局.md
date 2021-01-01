#### flex布局

##### 一 .flex容器的属性

###### 1. flex-direction属性

语法
`flex-direction: row | row-reverse | column | column-reverse`

`flex-direction` 决定的是`flex` 布局的方向,是横向(row)还是竖向(`column`)
首先我们得明白 `flex` 布局的顺序: 从左到右, 从上到下
![](E:\notes\pictures\flex布局\flex-direction.png)

###### 2. flex-wrap属性

语法:

`flex-wrap: no-wrap | wrap | wrap-reverse`
`wrap` : 空间不足时换行显示
`no-wrap` : 空间不足也不换行, 挤压元素
`wrap-reverse `: 与 `flex-direction` 定义的反方向换行

###### 3. flex-flow 属性

语法：
`flex-flow: <‘flex-direction’> || <‘flex-wrap’>`

这是`flex-direction`和`flex-wrap`的缩写属性

demo：

```css
.wrap {
 display: flex;
  flex-flow: row-reverse wrap-reverse;
}
```

###### 4. justify-content属性

语法：

`justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly`

`flex-start`

![](E:\notes\pictures\flex布局\flex-start.png)

`flex-end`
![](E:\notes\pictures\flex布局\flex-end.png)

`center`

![](E:\notes\pictures\flex布局\center.png)

`space-between`

两端对齐,多余空间在中间分配

![](E:\notes\pictures\flex布局\space-between.png)

`space-around`

左右的间隙等于中间元素的间距的一半

![](E:\notes\pictures\flex布局\space-around.png)

`space-evenly`

左右和中间的间隙都平均分配

![](E:\notes\pictures\flex布局\space-evenly.png)

###### 5.align-items属性

语法：

`align-items: stretch | flex-start | flex-end | center | baseline;`

声明子元素在竖直方向上的对齐方式

`stretch:`

默认值 ,  根据子元素的高度拉深

`flex-start:`

与文档流方向相关, 表现为顶部对齐

`flex-end:`

与文档流方向相关, 表现为底部对齐

`center:`

表现为竖直方向上居中对齐

`baseline:`

表现为所有flex子项都相对于 `flex` 容器的基线对齐。

###### 6.align-content属性

和 `justify-content` 属性相似, 可以看做竖直方向上的 `justify-content` , 但是需要注意一点, 当只有单行元素的时候 `align-content` 属性是不生效的.

##### 二.` flex` 子元素的属性

###### 1.order属性

修改 `order` 值可以改变子元素的排列顺序。

语法：

`order: <integer> 默认值0`

`.box3 {order: -1}`

![](E:\notes\pictures\flex布局\order属性.png)

###### 2.flex-grow属性

`grow` 是拓展的意思, 给元素设置后会按照 `flex-grow` 的属性值进行宽度拓展

语法：

```flex-grow:<number>; /* 数值，可以是小数，默认值是 0 */```

可以把所有的剩余空间当做1, 如果所有元素的`flex-grow`值之和小于1,就按值分配空间,并不是必须占据完剩余空间.

如果所有元素的`flex-grow`值大于1, 则将剩余空间按各个元素的`flew-grow`值的比例进行分配剩余空间.

###### 3.flex-shrink属性

和grow是相反的关系, grow是按照数值比例进行放大, shrink是按照一定数值比例进行收缩

*语法 flex-shrink:<number> / 数值，默认值是 1 /*

参考`flex-grow`属性, 一个放大一个缩小的关系.

###### 4.flex-basis属性

*语法flex-basis:<length>|auto     / auto是默认值 /*

默认值是`auto`,此时,元素的宽度受到以下属性影响, 同时设置`flex-basis`和`width`内容宽度超过width设置值后, width是表现无效的.

- `box-sizing`盒模型（默认是content-box）；
- `width`/`min-width`/`max-width`等宽度属性；
- `content`内容（min-content最小宽度）；

`flex-basis`属性除了接受数值,还接受关键字值

```js
/* 根据flex子项的内容自动调整大小 */
flex-basis: content;

/* 内部尺寸关键字 */
flex-basis: fill;
flex-basis: max-content;
flex-basis: min-content;
flex-basis: fit-content;
```

但是使用关键值属性时应该注意其浏览器兼容性

```js
浏览器兼容性查询地址:
https://www.caniuse.com/
```

`flex-basis`属性的妙用, 替代`min-width`和`max-width`实现小于指定大小自动等分换行布局

```css
<style>
.container {
    display: flex;
    flex-wrap: wrap;
}
.item {
    flex-basis: 100px;
    flex-grow: 1;
}
</style>
<div class="container">
 <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
</div>
```

![](E:\notes\pictures\flex布局\flex-basis属性_1.png)

![](E:\notes\pictures\flex布局\flex-basis属性_2.png)

![](E:\notes\pictures\flex布局\flex-basis属性_3.png)

###### 5.flex属性

`flex`属性是`flex-grow`，`flex-shrink`和`flex-basis`的缩写。

语法:

flex: none | auto | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]

第一个属性值为: `flex-grow`, 第二第三个分别为: `flex-shrink`和`flex-basis`可省略

- `flex`默认值等同于`flex:0 1 auto`；
- `flex:none`等同于`flex:0 0 auto`；
- `flex:auto`等同于`flex:1 1 auto`；

###### 6. align-self属性

`align-self`声明的是但那个元素的竖直方向上的对齐方式, 与`align-item`不同的是, `align-item`是多所有子元素同时设置。
语法align-self: auto | flex-start | flex-end | center | baseline | stretch;

#####  三、小提示

在Flex布局中，`flex` 子元素的设置`float`，`clear`以及`vertical-align`属性都是没有用的。