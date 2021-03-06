CSS的过渡属性transition可以仅通过CSS来实现简单的动画效果，同时它是一个简写属性，由transition-property、transition-duration、transition-timing-function和transition-delay复合而成。

### 过渡属性

1. transition-property 指定应用过渡属性的名称。

```cpp
transition-property: all; // 默认为all，所有可被动画的属性都表现出过渡动画。
transition-property: none; // 没有动画效果
transition-property: width, height; //也可以取其他属性的值
```

1. transition-duration 属性以秒或毫秒为单位指定过渡动画所需的时间。默认值为 0s ，表示不出现过渡动画。

```cpp
transition-duration: 1s;
transition-duration: 1ms;
transition-duration: 1s, 10s, 10ms; // 可以应用多个值，对应于transition-property的多个属性，表示每个属性对应的延时时间
```

1. transition-timing-function 表示过渡动画的运动曲线。

```php
transition-timing-function: cubic-bezier(n, n, n, n); // 在bezier 函数中自定义 0 ~ 1 之间的数值
transition-timing-function: ease; // 默认值，慢速开始，中间变快，慢速结束；相当于 cubic-bezier(0.25, 0.1, 0.25, 1)。
transition-timing-function: linear; // 匀速运动；相当于 cubic-bezier(0, 0, 1, 1)。
transition-timing-function: ease-in; // 慢速开始；相当于 cubic-bezier(0.42, 0, 1, 1)。
transition-timing-function: ease-out; // 慢速结束；相当于 cubic-bezier(0, 0, 0.58, 1)
transition-timing-function: ease-in-out; // 慢速开始，慢速结束；相当于 cubic-bezier(0.42, 0, 0.58, 1)
transition-timing-function: step-start;
transition-timing-function: step-end;
transition-timing-function: steps(4, end);
```

1. transition-delay 表示过渡效果的延迟时间

```text
transition-delay: 3s;
```

### 简写属性

transition是上面四个过渡属性的简写，其中只有transition-duration是必填属性。

```text
transition: all 5s linear .2s; // 以空格隔开属性
transition: all 5s linear .2s, height 3s ease-in-out; // 可以以逗号隔开多个过渡。
```

### 使用场景

transition一般在css中配合:hover, :active等伪类使用,实现相应等动画效果。

```css
.app {
  width: 300px;
  transition: all 3s linear .2s;
}

.app:hover {
  width: 100;
}
```

类似上面这种简单的鼠标移到class=app的html元素上，会出现简单的动画。

### 过渡阶段

过渡分为两个阶段：前进（forward）和反向（reverse），下面会用具体的例子来详细讲述这两个阶段。

1. 只在非hover状态设置transition
   该状态下设置的transition认为设置了反向状态的过渡动画，即鼠标移到元素上又离开时的动画，而此时前进状态和反向状态保持一致，也就是说鼠标移到和移开元素都有过渡动画。

```css
.app {
  width: 300px;
  transition: all 3s linear .2s;
}

.app:hover {
  width: 100;
}
```

1. 只在hover状态下设置transition
   该状态下设置的transition认为设置了前进状态的过渡动画，而此时反向状态是没有动画的。也就是说鼠标移到元素上会有动画，移出元素没有动画，元素宽度会瞬间还原。

```css
.app {
  width: 300px;
}

.app:hover {
  width: 100;
  transition: all 3s linear .2s;
}
```

1. 同时在hover和非hover状态下都设置transition
   此时即设置了前进状态也设置了反向状态的动画，鼠标移到元素上动画持续1s,鼠标移出元素动画持续3s。

```css
.app {
  width: 300px;
 transition: all 3s linear .2s;
}

.app:hover {
  width: 100;
  transition: all 1s linear .2s;
}
```

1. 过渡状态切换时的取值
   当前进和反向状态切换时，如果上一个状态的动画还没有结束，下一个状态的起始值是上一个状态最后时刻的值，也就是说两个状态切换时动画会连续播放，不会发生突变。
   当父级元素正在过渡时如果子元素触发过渡动画，则子元素过渡状态的起始值是继承了父元素正在过渡时的值。
2. 隐式过渡
   指一个属性的改变引起另一个属性的改变时发生的过渡。
   此属性Chrome和Safari不支持，Firefox和IE支持。