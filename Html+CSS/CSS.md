#### **BFC**

一个独立的布局环境。可以理解为一个区域，在这个区域内的元素无论如何布局排版，都不影响区域外的元素。
以下方法都会触发 BFC：
`body` 根元素
浮动元素： `float` 除 `none` 以外的值
绝对定位元素：`position (absolute、fixed)` 
`display`为 `inline-block 、table-cells 、flex` 
`overflow` 除了 `visible`  以外的值(`hidden、auto、scroll`)

#### 定位

##### 一、static

> 该关键字指定元素使用正常的布局行为，即元素在文档常规流中当前的布局位置。此时 top、right、bottom、left 属性无效。

`static`是`position`的默认值。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS-position-static</title>
    <link rel="stylesheet" href="https://cdn.bootcss.com/normalize/8.0.0/normalize.css">
    <style>
        .container{
            background-color: #868686;
            width: 100%;
            height: 300px;
        }
        .content{
            background-color: yellow;
            width: 100px;
            height: 100px;
            position: static;
            left: 10px;/* 这个left没有起作用 */
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="content">
        </div>
    </div>
</body>
</html>
```

![1601385006901](E:\notes\pictures\定位\position_static.png)

对 `content` 的` position` 设定 `static` 后，`left` 就失效了，而元素（`content`）就以正常的 `normal flow` 形式呈现。

##### 二、 relative

该关键字下，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素未添加定位时所在位置留下空白）。`position:relative` 对 `table-*-group, table-row, table-column, table-cell, table-caption` 元素无效。

> ```html
><!DOCTYPE html>
> <html lang="en">
>  <head>
>      <meta charset="UTF-8">
>      <meta name="viewport" content="width=device-width, initial-scale=1.0">
>       <meta http-equiv="X-UA-Compatible" content="ie=edge">
>       <title>CSS-position-relative</title>  
>       <link rel="stylesheet" href="https://cdn.bootcss.com/normalize/8.0.0/normalize.css">
>       <style>
>              .container{
>                  background-color: #868686;
>                  width: 100%;
>                  height: 300px;
>              }
>             .content_0{
>                  background-color: yellow;
>                  width: 100px;
>                  height: 100px;               
>              }
>              .content_1{
>                  background-color: red;
>                  width: 100px;
>                  height: 100px;
>                 position: relative;/* 这里使用了relative  */            
>              }
>              .content_2{
>                  background-color: black;
>                  width: 100px;
>                  height: 100px;               
>              }
>          </style>
>      </head>
>      <body>
>          <div class="container">
>              <div class="content_0">    
>              </div>
>              <div class="content_1">    
>              </div>
>              <div class="content_2">    
>              </div>
>          </div>   
>    </body>
>    </html>
>  ```
>  
> ![1601385223016](E:\notes\pictures\定位\position_relative.png)

这是没有设置left、top等属性时，正常出现在normal flow中的位置。
接着添加left、top：

![1601385309580](E:\notes\pictures\定位\position_static_2.png)

可以看到，元素（content_1）的位置相对于其原位置（normal flow中的正常位置）进行了移动。

##### 三、absolute

> 不为元素预留空间，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。绝对定位的元素可以设置外边距（margin），且不会与其他边距合并。

个人理解：生成绝对定位的元素，其相对于 `static` 定位以外的第一个父元素进行定位,会脱离`normal flow`。**注意：是除了static外**

```html
 <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>CSS-position-static</title>
      <link rel="stylesheet" href="https://cdn.bootcss.com/normalize/8.0.0/normalize.css">
      <style>
         .container{
             background-color: #868686;
             width: 100%;
             height: 300px;
             margin-top: 50px;
         }
         .content{
             background-color: red;
             width: 100px;
             height: 100px;
             position: absolute;
             top: 10px;
         }
     </style>
 </head>
 <body>
     <div class="container">
         <div class="content">    
         </div>
     </div>
 </body>
 </html>
```

![1601385422493](E:\notes\pictures\定位\position_absolute.png)

##### 四、fixed

> 不为元素预留空间，而是通过指定元素相对于屏幕视口 `viewport` 的位置来指定元素位置。元素的位置在屏幕滚动时不会改变。打印时，元素会出现在的每页的固定位置。fixed属性会创建新的层叠上下文。当元素祖先的  `transform`  属性非  `none`  时，容器由视口改为该祖先。

个人理解：`fixed` 相对于 `window`固定，滚动浏览器窗口并不会使其移动，会脱离`normal flow`。

```html
 <!DOCTYPE html>
 <html lang="en">
 <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <meta http-equiv="X-UA-Compatible" content="ie=edge">
     <title>CSS-position-static</title>
     <link rel="stylesheet" href="https://cdn.bootcss.com/normalize/8.0.0/normalize.css">
     <style>
         .container{
             background-color: #868686;
             width: 100%;
             height: 1000px;
         }
         .content{
             background-color: yellow;
             width: 100px;
            height: 100px;
             position: fixed;/* 这里使用了fixed */
         }
     </style>
 </head>
 <body>
     <div class="container">
         <div class="content">    
         </div>
     </div>
 </body>
 </html>

position: fixed
```

##### 五、sticky

> 盒位置根据正常流计算(这称为正常流动中的位置)，然后相对于该元素在流中的 flow root（BFC）和 containing block（最近的块级祖先元素）定位。在所有情况下（即便被定位元素为 table`时`），该元素定位均不对后续元素造成影响。当元素 B 被粘性定位时，后续元素的位置仍按照 B 未定位时的位置来确定。position: sticky对 table元素的效果与 position: relative 相同。

因为各大浏览器对于`sticky` 的兼容问题，而且`JS`也可以实现这个功能，在这里就不进行深入了，了解一下就好。

##### 六、 inherit

> 规定应该从父元素继承 position 属性的值。

`inherit`  继承父元素，这个用得不多，所以也不继续深入了。

#### 层叠上下文

层叠上下文其实把它理解为 z 轴也没有问题，屏幕上面叠着一层层图层（不是所有的元素都是）。层叠水平则表示同一层层叠上下文对应的图层。

##### 一、创建

以下情况会创建层叠上下文（随着 CSS3 属性还在增加，本表不全）：

- z-index 不为 auto 的 position
- 定位元素 z-index
- 不为 auto 的 flex
- opacity 不为 1
- transform 不为 none
- perspective 不为 none
- filter 不为 none
- mix-blend-mode 不为 normal
- 带有 isolation: isolate
- will-change 不为 none
- 带有 -webkit-overflow-scrolling: touch

```html
<style>
.box {
  width: 100px;
  height: 100px;
  margin: 0 auto -50px;
}
.box1 {background: pink}
.box2 {background: grey}
.box1 {left: 10px}

.box1 { transform: translate(0,0) }
</style>

<div class="box box1">层叠上下文层级会高于普通元素</div> <!-- 粉色 -->
<div class="box box2"></div> <!-- 灰色 -->
```

![1601386609917](E:\notes\pictures\层叠上下文\层叠上下文层级会高于普通元素.png)



##### 二、同级层叠顺序

而当有两个层叠上下文时，它们就有了兄弟和父子关系（假设现在都处于同级层叠水平）。

**当为兄弟关系时**（层叠上下文的兄弟关系，非 DOM 的兄弟），它们总是 **后者居上** 的。

```html
<style>
.box {
  width: 100px;
  height: 100px;
  margin: 0 auto -50px;
}
.item {
  /* 两个 dom 中子级创建层叠上下文，构成兄弟关系的层叠水平 */
  transform: translate(0,0);
  width: 90px;
  height: 90px;
  top: -10px;
}
.box1 {background: pink}
.box2 {background: grey}
.item1 {background: red}
.item2 {background: green}
.item1 {left: -10px;}
.item2 {left: -20px;}
</style>

<div class="box box1"> <!-- 粉色 -->
  <div class="item item1">item1</div> <!-- 红色 -->
</div>
<div class="box box2"> <!-- 灰色 -->
  <div class="item item2">item2</div> <!-- 绿色 -->
</div>

<!-- .item 变为层叠上下文，所以比 .box 这种普通元素层级更高. -->
<!-- 且 .item 遵循后者居上，所以 .item2 覆盖了 .item1 -->
```

![1601386927905](E:\notes\pictures\层叠上下文\同级层叠水平下的层叠顺序.png)

**当为父子关系时**，子级就存在父级的“作用域”内了，父级高我才高，不然我再高也没用。

```html
<style>
.box { position: relative; z-index: 0 }
.item1 { z-index: 999; }
/* 紧跟上例，本来 .item2 由谁后谁上的原则位于上面。 */
/* 当现在其父级 .box 也创建的层叠上下文，且遵循谁后谁上，因此 .box2 要高于 .box1。 */
/* 此处 .item1 的父级已经低于 .box2 了，本身层级再高也还是在 .box1 的范围内而已。 */
</style>
```

![1601386985083](E:\notes\pictures\层叠上下文\当为父子关系时层叠水平.png)

注：此处 `position: relative`; 但不写 z-index: 0（即 z-index: auto），它会覆盖普通元素，但并不会创建层叠上下文。 下面这个也是类似的例子，

```html
.box {
  position: relative;
  margin: 0 0 10px;
}
.box2 { z-index: 0; }
/* 只有 z-index 不为 auto 才创建层叠上下文，所以 .box2 创了，.box1 没创 */
.item {
  position: relative;
  z-index: -1;
}
```

![1601387095590](E:\notes\pictures\层叠上下文\当父级为层叠上下文时，子级无法再低于父级的层级.png)

##### 三、不同级层叠顺序

既 z-index 不为 `auto` 的情况，这时它们总是 **谁大谁上** 的。

```html
<style>
.box1 { z-index: 2; }
/* 这个就很好理解了，.box 现在是兄弟关系，.box1 的 z-index 更大，那么它就更高 */
</style>
```

![1601387147466](E:\notes\pictures\层叠上下文\都为层叠上下文时，index 将决定他们的层级.png)

#### 边距折叠

##### 一、外边距折叠

相邻的两个或多个外边距 (margin) 在垂直方向会合并成一个外边距（margin）
相邻：没有被非空内容、padding、border 或 clear 分隔开的margin特性. 非空内容就是说这元素之间要么是兄弟关系或者父子关系

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <style type="text/css">
            *{margin:0;padding:0;}
            #div1{
                border: 3px solid yellow;
                height: 200px;
                margin-top: 20px;
            }
            #div2{
                height: 100px;
                background: blue;
                margin-top: 20px;
            }
            #div3{
                height: 50px;
                width: 50%;
                background: green;
                margin-top: 50px;
            }
        </style>
    </head>
    <body>
        <div id="div1">
            <div id="div2">
                <div id="div3">
                </div>
            </div>
   </div>
    </body>
</html>
```

![](E:\notes\pictures\边距折叠\外边距折叠.png)


因为div2与div3的外边距是相邻的（**是父子关系的相邻**），当div2 margin-top为20,div3的margin-top也为50,此时div2与div3的外边距会合并，就是折叠。
而div1与div2的外边距不是相邻的（div1有border），它们便不会折叠。

##### 二、合并计算

参加折叠的margin都是正值：取其中 margin 较大的值为最终 margin 值。

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>边距折叠</title>
    </head>
    <body>
        <div style="height:90px; margin-bottom:99px; width:90px; background-color: red;">X</div>
        <div style="height:90px; margin-top:100px; width:90px; background-color: blue;">Y</div>
    </body>
</html>
```

![](E:\notes\pictures\边距折叠\垂直方向外边距合并计算.png)

参与折叠的 margin 都是负值：取的是其中绝对值较大的，然后，从 0 位置，负向位移。

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>边距折叠</title>
    </head>
    <body>
        <div style="height:90px; margin-bottom:-10px; width:90px; background-color: red;">X</div>
        <div style="height:90px; margin-top:-30px;width:70px; background-color: blue;">Y</div>
    </body>
</html>
```

参与折叠的 margin 中有正值，有负值：先取出负 margin 中绝对值中最大的，然后，和正 margin 值中最大的 margin 相加。

![](E:\notes\pictures\边距折叠\垂直方向外边距合并计算_2.png)

#### 浮动布局

##### 一、浮动

浮动元素会向左/右偏移，直至外边界碰到容器或另一个元素的边缘。 浮动会使得元素脱离文档流，后面元素进行布局时，前面的浮动元素就像不存在一样。

![](E:\notes\pictures\浮动布局\浮动.jpg)

如果右侧没有足够空间，浮动元素就会下坠，直到有足够的空间（折行）。 如果浮动元素有着不同的高度，那么可能在下坠过程中卡在某个位置。

![](E:\notes\pictures\浮动布局\浮动_2.jpg)

##### 二、清除浮动

虽然浮动也会使元素脱离文档流，但与绝对定位不同，后续元素仍然会为浮动元素腾出空间。 这可以导致文字环绕的效果，这也是浮动的初衷之一。

![](E:\notes\pictures\浮动布局\清除浮动.jpg)

如果希望某一行停止环绕，可以为该行设置清除浮动（clear）。它有四种值：left, right, both, none，表示哪个方向不应当与浮动元素相邻。 CSS渲染器通过添加margin-top来达到这个效果。例如：

![](E:\notes\pictures\浮动布局\清除浮动_2.jpg)

##### 三、浮动容器

浮动元素不占据父容器的空间。 这使得父容器大小为零，当然父容器的边框和背景就会失效：

![](E:\notes\pictures\浮动布局\浮动容器.jpg)

但是有没有发现我们为任何一个元素清除浮动都打不到效果。这时我们需要一个额外的空元素， 并设置clear:both：

![](E:\notes\pictures\浮动布局\浮动容器_2.jpg)

通过额外的元素我们达到了效果，为此 `Bootstrap`可以提供了 `clearfix`类。` Bootstrap` 中这个空元素可以这样写：

```html
<div class="clearfix"></div>
```

替代方案

让容器也浮动

但强迫症患者一定不喜欢这个额外的`div`，一个替代方式是将容器也浮动起来。 当然这会造成后续元素的布局也需要浮动，所以有些网站里几乎所有元素都在浮动！

设置容器overflow

将容器的 `overflow` 设置为`auto`或 `hidden` 也可以达到效果。 但设置`overflow` 有时候会产生我们不希望的行为。

##### 四、`CSS` 伪元素

为了不要那个额外的空元素，我们可以用`CSS`来为容器添加一个伪元素：

```css
.clear:after {
    content: ".";
    height: 0;
    visibility: hidden;
    display: block;
    clear: both;
}
```

在IE6以下的浏览器中，还需要设置height: 1%（IE BUG）。

其实和空元素的原理是一样的...只是这个元素是运行时产生的，不过代码还是整洁了。 之所以`display:block` ，是因为clear的原理是自动添加margin-top， 而该属性对行内元素是不起作用的。

#### flex布局

##### 一 .flex容器的属性

###### 1. flex-direction属性

语法
`flex-direction: row | row-reverse | column | column-reverse`

`flex-direction` 决定的是`flex` 布局的方向,是横向(row)还是竖向(column)
首先我们得明白flex布局的顺序: 从左到右, 从上到下
![](E:\notes\pictures\flex布局\flex-direction.png)

###### 2. flex-wrap属性

语法:

`flex-wrap: no-wrap | wrap | wrap-reverse`
wrap: 空间不足时换行显示
no-wrap: 空间不足也不换行, 挤压元素
wrap-reverse: 与flex-direction定义的反方向换行

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

默认值,根据子元素的高度拉深

`flex-start:`

与文档流方向相关, 表现为顶部对齐

`flex-end:`

与文档流方向相关, 表现为底部对齐

`center:`

表现为竖直方向上居中对齐

`baseline:`

表现为所有flex子项都相对于flex容器的基线（字母x的下边缘）对齐。

###### 6.align-content属性

和justify-content属性相似, 可以看做竖直方向上的justify-content, 但是需要注意一点, 当只有单行元素的时候align-conteng属性是不生效的.

##### 二. flex子元素的属性

###### 1.order属性

修改order值可以改变子元素的排列顺序.

语法：

`order: <integer> 默认值0`

`.box3 {order: -1}`

![](E:\notes\pictures\flex布局\order属性.png)

###### 2.flex-grow属性

grow是拓展的意思, 给元素设置后会按照flex-grow的属性值进行宽度拓展

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

```shell
/* 根据flex子项的内容自动调整大小 */
flex-basis: content;

/* 内部尺寸关键字 */
flex-basis: fill;
flex-basis: max-content;
flex-basis: min-content;
flex-basis: fit-content;
```

但是使用关键值属性时应该注意其浏览器兼容性

```
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

在Flex布局中，flex子元素的设置`float`，`clear`以及`vertical-align`属性都是没有用的。

#### grid布局

#### 页面渲染机制

当我们在浏览器里输入一个 URL 后，最终会呈现一个完整的网页。这中间会经历如下的过程:

##### 一、HTML 的加载

输入 URL 后，最先拿到的是 HTML 文件。HTML是一个网页的基础，所以要在最开始的时候下载它。HTML下载完成以后就会开始对它进行解析。

##### 二、其他静态资源下载

HTML 在解析的过程中，如果发现 HTML 文本里面夹杂的一些外部的资源链接，比如 CSS、JS 和图片等时，会立即启用别的线程下载这些静态资源。这里有个特殊的是 JS 文件，当遇到 JS 文件的时候，HTML 的解析会停下来，等 JS 文件下载结束并且执行完，HTML 的解析工作再接着来。这样做是因为 JS 里可能会出现修改已经完成的解析结果，有白白浪费资源的风险，所以 HTML 解析器干脆等 JS 折腾完了再干。

##### 三、DOM 树构建

在 HTML 解析的同时，解析器会把解析完的HTML转化成DOM 对象，再进一步构建 DOM 树。

##### 四、CSSOM 树构建

当 CSS 下载完，CSS 解析器就开始对 CSS 进行解析，把 CSS 解析成 CSS 对象，然后把这些 CSS 对象组装起来，构建出一棵 CSSOM 树。

##### 五、渲染树构建

DOM 树和 CSSOM 树都构建完成以后，浏览器会根据这两棵树构建出一棵渲染树。

##### 六、布局计算

​    渲染树构建完成以后，所有元素的位置关系和需要应用的样式就确定了。这时候浏览器会计算出所有元素的大小和绝对位置。
​    渲染布局计算完成以后，浏览器就可以在页面上渲染元素了。比如从 (x1, y1) 到（x2, y2）的正方形区域渲染成蓝色。经过渲染引擎的处理后，整个页面就显示在了屏幕上。

##### 七、DOM 树的构建

​    页面中的每一个 HTML 标签，都会被浏览器解析成一个对象，我们称它为文档对象（Document Object）。HTML 的本质是一个嵌套结构，在解析的时候会把每个文档对象用一个树形结构组织起来，所有的文档对象都会挂在一个叫做 Document 的东西上，这种组织方式就是 HTML 最基础的结构–文档对象模型（DOM），这棵树里面的每个文档对象就叫做 DOM 节点。
​    在 HTML 加载的过程中，DOM 树就在开始构建了。构建的过程是先把 HTML 里每个标签都解析成 DOM 节点（每个标签的属性、值和上下文关系等都在这个文档对象里），然后使用深度遍历的方法把这些对象构造成一棵树。

eg:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <link rel="stylesheet" href="./index.css">
</head>
<body>
    <div class="header">
        <span class="page-name">文章详情页</span>
    </div>
    <div class="content">
        <h1 class="title">文章标题</h1>
        <div class="article">
            <p class="graph">吃葡萄不吐葡萄皮</p>
            <img src="./test.jpg" alt="文章插图">
            <p class="graph">不吃葡萄倒吐葡萄皮</p>
        </div>
    </div>
</body>
</html>
```

在构建 DOM 树的时候，就是从最外层 HTML 节点开始，按深度优先的方式构建。之所以用深度优先，是因为 HTML在加载的时候是自上而下的，最先加载的是根节点<html>，然后是根节点的第一个子节点<head>，再然后是head的第一个子节点<meta>…head构建完成后再去构建 body 部分的内容，以此类推。使用深度优先的方式构建这棵树就和文档的加载顺序吻合了。最后，上面这个 html 结构就会生成一棵 DOM 树。

##### 八、CSSOM 树的构建

在浏览器构建 DOM 树的同时，如果样式也加载完成了，那么 CSSOM 树也在同步地构建。CSS 树和 DOM 类似，它的树形结构记录着所有样式的信息。

我们以给上面的 HTML 加上如下的样式：

```css
body{
    font-size: 16px;
}
// 去掉所有p元素的内外边距
p{
    margin: 0;
    padding: 0;
}
// 页面头部行高50px，文本垂直居中，隐藏
.header{
    height: 50px;
    line-height: 50px; 
    display: none;
    text-align: center;
}
.header .page-name{
    font-size: 20px;
}
// 文本区域左右两边留10px空白
.content{
    padding: 0 10px; 
}
.contetn .title{
    font-seize: 20px;
}
// 内容区行高30px
.content .graph{
    line-height: 30px; 
}
// 文章中的图片用作块级元素，水平居中
.content img{
    display: block;
    margin: 0 auto;
}
```

我们就以这一组样式为例，这样一组样式中有公用的样式 p 和 body，有标题栏 .header 部分的样式，还有内容区 .content 部分的样式。
渲染的大致过程、DOM 树的构建和 CSSOM 树的构建基本完成。

#### 性能优化之白屏时间

##### 一、概念

白屏时间：即用户点击一个链接或打开浏览器输入URL地址后，从屏幕空白到显示第一个画面的时间。

##### 二、白屏的过程

###### 1. DNS Lookup

> DNS Lookup 即浏览器从DNS服务器中进行域名查询。

浏览器会先对页面进行域名解析，获取到服务器的IP地址后，进而和服务器进行通信。

**Tips:** 通常在整个加载页面的过程中，浏览器会多次进行DNS Lookup，包括页面本身的域名查询以及在解析HTML页面时加载的JS、CSS、Image、Video等资源产生的域名查询。

###### 2. 建立TCP请求连接

浏览器和服务端TCP请求建立的过程，是基于TCP/IP，该协议由网络层的IP和传输层的TCP组成。IP是每一台互联网设备在互联网中的唯一地址。
TCP通过**三次握手**建立连接，并提供可靠的数据传输服务。

###### 3. 服务端请求处理响应

​    在TCP连接建立后，Web服务器接受请求，开始进行处理，同时浏览器端开始等待服务器的处理响应。
​    Web服务器根据请求类型的不同，进行相应的处理。静态资源如图片、CSS文件、静态HTML直接进行响应；如其他注册的请求转发给相应的应用服务器，进行如数据处理、缓存中取数据，将数据按照约定好的格式响应给浏览器。

> 在大型应用中，通常为分布式服务架构，应用服务器的处理有可能经过很多个系统的中间件，最终获取到需要的数据

###### 4. 客户端下载、解析、渲染显示页面

在服务器返回数据后，客户端浏览器接收数据，进行HTML下载、解析、渲染显示。

- a. 如果是Gzip包，则先解压为HTML
- b. 解析HTML的头部代码，下载头部代码中的样式资源文件或脚本资源文件
- c. 解析HTML代码和样式文件代码，构建HTML的DOM树以及与CSS相关的CSSOM树
- d. 通过遍历DOM树和CSSOM树，浏览器依次计算每个节点的大小、坐标、颜色等样式，构造渲染树
- e. 根据渲染树完成绘制过程

浏览器下载HTML后，首先解析头部代码，进行样式表下载，然后继续向下解析HTML代码，构建DOM树，同时进行样式下载。当DOM树构建完成后，立即开始构造CSSOM树。理想情况下，样式表下载速度够快，DOM树和CSSOM树进入一个并行的过程，当两棵树构建完毕，构建渲染树，然后进行绘制。

**Tips:**浏览器安全解析策略对解析HTML造成的影响：

- 当解析HTML时遇到内联JS代码，会阻塞DOM树的构建

- **特别悲惨的情况：** 当CSS样式文件没有下载完成时，浏览器解析HTML遇到了内联JS代码，此时！！！根据浏览器的安全解析策略，浏览器暂停JS脚本执行，暂停HTML解析。直到CSS文件下载完成，完成CSSOM树构建，重新恢复原来的解析。

  > 一定要合理放置JS代码！！！

##### 三、白屏-性能优化

至此，我们已经了解了从浏览器在打开一个链接开始，到屏幕展示的过程-白屏时间的历程，那这对每个环节中发生的事情，我们可以有针对性的进行相关的优化。

###### 1. DNS解析优化

针对DNS Lookup环节，我们可以针对性的进行DNS解析优化。

- DNS缓存优化
- DNS预加载策略
- 稳定可靠的DNS服务器

###### 2. TCP网络链路优化

针对网络链路的优化，好像除了花钱没有什么更好的方式！

###### 3. 服务端处理优化

服务端的处理优化，是一个非常庞大的话题，会涉及到如Redis缓存、数据库存储优化或是系统内的各种中间件以及Gzip压缩等...

###### 4. 浏览器下载、解析、渲染页面优化

根据浏览器对页面的下载、解析、渲染过程，可以考虑一下的优化处理：

- 尽可能的精简HTML的代码和结构
- 尽可能的优化CSS文件和结构
- 一定要合理的放置JS代码，尽量不要使用内联的JS代码

#### FOUC

`FOUC` 是 `Flash of Unstyled Content` 的首字母缩略词，表示**文档样式短暂失效**，对于这种现象，我们在前端 `UI` 开发时应该尽量避免出现。

前端 `UI` 开发时，在引用 `CSS` 的过程中，如果引用的方法不当或者位置引用不对，就会导致某些页面在 `IE` 浏览器中出现一些奇怪的现象：用户定义样式表加载之前浏览器使用默认样式显示文档，用户样式加载渲染之后再重新显示文档，造成页面闪烁。

我们将这种显示页面内容的瞬间进行样式切换的闪烁现象称之为文档样式短暂失效，简称 `FOUC`。

##### 一、原因

出现 `FOUC` 的原因大致有以下几种：

- 使用 `@import` 的方式导入样式表
- 将样式表放在页面底部
- 有几个样式表，放在 `HTML` 结构的不同位置

其实原理很清楚：当样式表晚于结构性 `HTML` 加载，在加载到此样式表时，页面将停止之前的渲染，当样式表被下载和解析后，页面将被重新渲染，也就出现了短暂的闪烁现象。

##### 二、解决方案

其实解决 `FOUC` 问题的方法很简单，就是使用 `<link>` 标签将外部样式表的引入放在文档的 `<head>` 头部，这也是我们在页面中引入外部 `CSS` 样式表时推荐使用 `<link>` 标签的原因之一。

#### 异步加载

##### 一、script标签的位置

传统的做法是：所有script元素都放在head元素中，必须等到全部js代码都被下载、解析、执行完毕后，才能开始呈现网页的内容（浏览器在遇到<body>标签时才开始呈现内容），这在需要很多js代码的页面来说，会造成浏览器在呈现页面时出现明显的延迟，而延迟期间的浏览器窗口将是一片空白。因此。一般把script标签放在</body>标签前面。

##### 二、嵌入脚本与外部脚本

尽可能使用外部脚本，理由如下：

(1)将所有js文件放在一个文件夹中，再不触及 `HTML` 代码的情况下编辑js文件，便于维护。

(2)浏览器可以根据具体的设置所有外部`js` 文件，同一个文件只需下载一次，可以加快页面加载的速度。

##### 三、async和defer

###### 1、defer="defer"和async="true/false"

html4.0中定义了defer；html5.0中定义了async。

(1)没有defer或async，浏览器会立即加载并执行指定的JS脚本，也就是说，不等待后续载入的文档元素，读到JS脚本就加载并执行。

(2)有async，加载后续文档元素的过程将和JS的加载与执行并行进行（异步）。

(3)有defer，加载后续文档元素的过程将和JS的加载并行进行（异步），但JS的执行要在所有文档元素解析完成之后，DOMContentLoaded 事件触发之前完成。

###### 2、defer和async的共同点：

(1)不会阻塞文档元素的加载。

(2)使用这两个属性的脚本中不能调用document.write方法。

(3)允许不定义属性值，仅仅使用属性名。

(4)只适用于外部脚本（虽然IE4-IE7还支持对嵌入脚本的defer属性，但在IE8及之后的版本就只支持外部脚本，对不支持的会直接忽略defer属性，因此把延迟脚本放在页面底部仍然是最佳选择）。

###### 3、defer和async的不同点：

(1)每一个 `async `属性的脚本一旦加载完毕就会立刻执行，一定会在 `window.onload` 之前执行，但可能在`document`的 `DOMContentLoaded` 之前或之后执行。不保证按照指定它们的顺序来执行，如果JS有依赖性就要注意了。指定异步脚本的目的是不让页面等待两个脚本下载和执行，从而异步加载页面其他内容，因此，建议异步脚本不要在加载期间修改DOM。

2)每一个defer属性的脚本都是在文档元素完全载入后，一般会按照原本的顺序执行，同时一般会在document的DOMContentLoaded之前执行，相当于window.onload，但应用上比 window.onload 更灵活！实际上，defer 更接近于DomContentLoad。事实上，延迟脚本不一定会按顺序执行，也不一定会在DOMContentLoaded事件触发之前执行，因此最好只包含一个延迟脚本。

##### 四、动态创建script

在没有定义defer和async之前，异步加载的方式是动态创建script，通过window.onload方法确保页面加载完毕再将script标签插入到DOM中。

```js
function addScriptTag(src){
	var script = document.createElement('script');
	script.setAttribute("type","text/javascript");
	script.src = src;
	document.body.appendChild(script);
}
window.onload = function(){
	addScriptTag("js/index.js");
}
```

#### 重绘与回流

![img](https://mmbiz.qpic.cn/mmbiz_png/ibsfLhQMgy09mo4iap5DITrL1hvoNWJGDOteXH29tB4pgV8uPQfaIy1RY20agNicPMskbhQdAXGuhWumpjB9AEGwA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



从上面这个图上，我们可以看到，浏览器渲染过程如下：

1、解析HTML，生成DOM树，解析CSS，生成CSSOM树；
2、将DOM树和CSSOM树结合，生成渲染树(Render Tree)；
3、Layout(回流):根据生成的渲染树，进行回流(Layout)，得到节点的几何信息（位置，大小）；
4、Painting(重绘):根据渲染树以及回流得到的几何信息，得到节点的绝对像素；
5、Display:将像素发送给GPU，展示在页面上。（这一步其实还有很多内容，比如会在GPU将多个合成层合并为同一个层，并展示在页面中。而css3硬件加速的原理则是新建合成层，这里我们不展开，之后有机会会写一篇博客）。

渲染过程看起来很简单，让我们来具体了解下每一步具体做了什么。

##### 一、生成渲染树

![img](https://mmbiz.qpic.cn/mmbiz_png/ibsfLhQMgy09mo4iap5DITrL1hvoNWJGDO0L0mcVib7uPn4UKN93e0n9HuoqanjuFV1JA7UIDHfibYmAX6McTGx7cw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

为了构建渲染树，浏览器主要完成了以下工作：

1.从DOM树的根节点开始遍历每个可见节点。
2.对于每个可见的节点，找到CSSOM树中对应的规则，并应用它们。
3.根据每个可见节点以及其对应的样式，组合生成渲染树。

第一步中，既然说到了要遍历可见的节点，那么我们得先知道，什么节点是不可见的。不可见的节点包括：

1、一些不会渲染输出的节点，比如script、meta、link等。
2、一些通过css进行隐藏的节点。比如display:none。注意，利用visibility和opacity隐藏的节点，还是会显示在渲染树上的。只有display:none的节点才不会显示在渲染树上。

**注意**：渲染树只包含可见的节点

##### 二、回流

前面我们通过构造渲染树，我们将可见DOM节点以及它对应的样式结合起来，可是我们还需要计算它们在设备视口(viewport)内的确切位置和大小，这个计算的阶段就是回流。

为了弄清每个对象在网站上的确切大小和位置，浏览器从渲染树的根节点开始遍历，我们可以以下面这个实例来表示：

```
<!DOCTYPE html><html>  <head>    <meta name="viewport" content="width=device-width,initial-scale=1">    <title>Critial Path: Hello world!</title>  </head>  <body>    <div style="width: 50%">      <div style="width: 50%">Hello world!</div>    </div>  </body></html>
```

我们可以看到，第一个div将节点的显示尺寸设置为视口宽度的50%，第二个div将其尺寸设置为父节点的50%。而在回流这个阶段，我们就需要根据视口具体的宽度，将其转为实际的像素值。（如下图）

![img](https://mmbiz.qpic.cn/mmbiz_png/ibsfLhQMgy09mo4iap5DITrL1hvoNWJGDOxT5Q6MnMYIVIWSiaic8aFH8ryYj7ke7Z7oyb20V46O31IZJl74ibf2kJA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

##### 三、重绘

　　最终，我们通过构造渲染树和回流阶段，我们知道了哪些节点是可见的，以及可见节点的样式和具体的几何信息(位置、大小)，那么我们就可以将渲染树的每个节点都转换为屏幕上的实际像素，这个阶段就叫做重绘节点。

##### 四、何时发生回流重绘

　　我们前面知道了，回流这一阶段主要是计算节点的位置和几何信息，那么当页面布局和几何信息发生变化的时候，就需要回流。比如以下情况：
~ 添加或删除可见的DOM元素；
~ 元素的位置发生变化；
~ 元素的尺寸发生变化（包括外边距、内边框、边框大小、高度和宽度等）；
~ 内容发生变化，比如文本变化或图片被另一个不同尺寸的图片所替代；
~ 页面一开始渲染的时候（这肯定避免不了）；
~ 浏览器的窗口尺寸变化（因为回流是根据视口的大小来计算元素的位置和大小的）。

**注意**：回流一定会触发重绘，而重绘不一定会回流

根据改变的范围和程度，渲染树中或大或小的部分需要重新计算，有些改变会触发整个页面的重排，比如，滚动条出现的时候或者修改了根节点。

##### 五、浏览器的优化机制

现代的浏览器都是很聪明的，由于每次重排都会造成额外的计算消耗，因此大多数浏览器都会通过队列化修改并批量执行来优化重排过程。浏览器会将修改操作放入到队列里，直到过了一段时间或者操作达到了一个阈值，才清空队列。但是！**当你获取布局信息的操作的时候，会强制队列刷新**，比如当你访问以下属性或者使用以下方法：

1.offsetTop、offsetLeft、offsetWidth、offsetHeight
2.scrollTop、scrollLeft、scrollWidth、scrollHeight
3.clientTop、clientLeft、clientWidth、clientHeight
4.getComputedStyle()
5.getBoundingClientRect
6.具体可以访问这个网站：https://gist.github.com/paulirish/5d52fb081b3570c81e3a

以上属性和方法都需要返回最新的布局信息，因此浏览器不得不清空队列，触发回流重绘来返回正确的值。因此，我们在修改样式的时候，**最好避免使用上面列出的属性，他们都会刷新渲染队列**。如果要使用它们，最好将值缓存起来。

##### 六、减少回流和重绘

好了，到了我们今天的重头戏，前面说了这么多背景和理论知识，接下来让我们谈谈如何减少回流和重绘。

##### 七、最小化重绘和重排

由于重绘和重排可能代价比较昂贵，因此最好就是可以减少它的发生次数。为了减少发生次数，我们可以合并多次对DOM和样式的修改，然后一次处理掉。考虑这个例子

```shell
const el = document.getElementById('test');el.style.padding = '5px';el.style.borderLeft = '1px';el.style.borderRight = '2px';
```

例子中，有三个样式属性被修改了，每一个都会影响元素的几何结构，引起回流。当然，大部分现代浏览器都对其做了优化，因此，只会触发一次重排。但是如果在旧版的浏览器或者在上面代码执行的时候，有其他代码访问了布局信息(上文中的会触发回流的布局信息)，那么就会导致三次重排。

因此，我们可以合并所有的改变然后依次处理，比如我们可以采取以下的方式：

###### 1、使用cssText：

```
const el = document.getElementById('test');el.style.cssText += 'border-left: 1px; border-right: 2px; padding: 5px;';
```

###### 2、修改CSS的class：

```
const el = document.getElementById('test');el.className += ' active';
```

##### 八、批量修改DOM

当我们需要对DOM对一系列修改的时候，可以通过以下步骤减少回流重绘次数：

~ 使元素脱离文档流；
~ 对其进行多次修改；
~ 将元素带回到文档中。

该过程的第一步和第三步可能会引起回流，但是经过第一步之后，对DOM的所有修改都不会引起回流，因为它已经不在渲染树了。

有三种方式可以让DOM脱离文档流：

1.隐藏元素，应用修改，重新显示；
2.使用文档片段(document fragment)在当前DOM之外构建一个子树，再把它拷贝回文档。
3.将原始元素拷贝到一个脱离文档的节点中，修改节点后，再替换原始的元素。

考虑我们要执行一段批量插入节点的代码：

```js
function appendDataToElement(appendToElement, data) {    let li;    for (let i = 0; i < data.length; i++) {        li = document.createElement('li');        li.textContent = 'text';        appendToElement.appendChild(li);    }}const ul = document.getElementById('list');appendDataToElement(ul, data);
```

如果我们直接这样执行的话，由于每次循环都会插入一个新的节点，会导致浏览器回流一次。

我们可以使用这三种方式进行优化:

**隐藏元素，应用修改，重新显示**

这个会在展示和隐藏节点的时候，产生两次重绘

```shell
function appendDataToElement(appendToElement, data) {    let li;    for (let i = 0; i < data.length; i++) {        li = document.createElement('li');        li.textContent = 'text';        appendToElement.appendChild(li);    }}const ul = document.getElementById('list');ul.style.display = 'none';appendDataToElement(ul, data);ul.style.display = 'block';
```

**使用文档片段(document fragment)在当前DOM之外构建一个子树，再把它拷贝回文档**

```shell
const ul = document.getElementById('list');const fragment = document.createDocumentFragment();appendDataToElement(fragment, data);ul.appendChild(fragment);
```

**将原始元素拷贝到一个脱离文档的节点中，修改节点后，再替换原始的元素。**

```shell
const ul = document.getElementById('list');
const clone = ul.cloneNode(true);appendDataToElement(clone, data);ul.parentNode.replaceChild(clone, ul);
```

对于上述那种情况，我写了一个demo来测试修改前和修改后的性能。然而实验结果不是很理想。

**原因**：原因其实上面也说过了，浏览器会使用队列来储存多次修改，进行优化，所以对这个优化方案，我们其实不用优先考虑。

##### 九、避免触发同步布局事件

上文我们说过，当我们访问元素的一些属性的时候，会导致浏览器强制清空队列，进行强制同步布局。举个例子，比如说我们想将一个p标签数组的宽度赋值为一个元素的宽度，我们可能写出这样的代码：

```shell
function initP() {    for (let i = 0; i < paragraphs.length; i++) {        paragraphs[i].style.width = box.offsetWidth + 'px';    }}
```

这段代码看上去是没有什么问题，可是其实会造成很大的性能问题。在每次循环的时候，都读取了`box`的一个`offsetWidth`属性值，然后利用它来更新p标签的width属性。这就导致了每一次循环的时候，浏览器都必须先使上一次循环中的样式更新操作生效，才能响应本次循环的样式读取操作。每一次循环都会强制浏览器刷新队列。我们可以优化为:

```shell
const width = box.offsetWidth;function initP() {    for (let i = 0; i < paragraphs.length; i++) {        paragraphs[i].style.width = width + 'px';    }}
```

同样，我也写了个demo来比较两者的性能差异。你可以自己点开这个demo体验下。这个对比差距就比较明显。
demo:http://t.cn/E4Dv0cB ，转了下短链接

**对于复杂动画效果,使用绝对定位让其脱离文档流**

对于复杂动画效果，由于会经常的引起回流重绘，因此，我们可以使用绝对定位，让它脱离文档流。否则会引起父元素以及后续元素频繁的回流。这个我们就直接上个例子。

示例地址：http://t.cn/E4DP765

打开这个例子后，我们可以打开控制台，控制台上会输出当前的帧数(虽然不准)。

![img](https://mmbiz.qpic.cn/mmbiz_png/ibsfLhQMgy09mo4iap5DITrL1hvoNWJGDONGiaI9cmOBFSMRmseCKXyLaw4t7az5N2YG67BiaTyZiahokm7nvetRrHQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

从上图中，我们可以看到，帧数一直都没到60。这个时候，只要我们点击一下那个按钮，把这个元素设置为绝对定位，帧数就可以稳定60。

##### 十、css3硬件加速（GPU加速）

比起考虑如何减少回流重绘，我们更期望的是，根本不要回流重绘。这个时候，css3硬件加速就闪亮登场啦！！

**划重点**：使用css3硬件加速，可以让transform、opacity、filters这些动画不会引起回流重绘 。但是对于动画的其它属性，比如background-color这些，还是会引起回流重绘的，不过它还是可以提升这些动画的性能。

本篇文章只讨论如何使用，暂不考虑其原理，之后有空会另外开篇文章说明。

###### 1、如何使用

常见的触发硬件加速的css属性：

\- transform

\- opacity

\- filters

\- Will-change

###### 2、效果

我们可以先看个例子。我通过使用chrome的Performance捕获了一段时间的回流重绘情况，实际结果如下图：

![img](https://mmbiz.qpic.cn/mmbiz_png/ibsfLhQMgy09mo4iap5DITrL1hvoNWJGDOicBr9atXH5ickK5D1bQuhnFw2Qw0eIx2ZK5YjjpRsjQicF6YZwic7VUbfA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

从图中我们可以看出，在动画进行的时候，没有发生任何的回流重绘。如果感兴趣你也可以自己做下实验。

###### 3、重点

1、使用 `css3` 硬件加速，可以让 `transform` 、`opacity`、`filters` 这些动画不会引起回流重绘
2、对于动画的其它属性，比如background-color这些，还是会引起回流重绘的，不过它还是可以提升这些动画的性能。

###### 4、css3硬件加速的坑

（1）、如果你为太多元素使用 `css3` 硬件加速，会导致内存占用较大，会有性能问题。
（2）、在 `GPU` 渲染字体会导致抗锯齿无效。这是因为`GPU` 和 `CPU` 的算法不同。因此如果你不在动画结束的时候关闭硬件加速，会产生字体模糊。

#### 基本数据类型

8种数据类型

#### 运算符优先级

