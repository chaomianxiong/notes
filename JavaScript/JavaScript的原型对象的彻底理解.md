更新于 2020-12-17

---

开篇先记住以下两点，再渐渐通过实例理解

1. `__proto__`和`constructor`属性是**对象**所独有的；
2. `prototype`属性是**函数**所独有的。

但是由于 `JS` 中函数也是一种对象，所以函数也拥有 `__proto__` 和 `constructor` 属性

#### 一、函数的原型对象

​    我们创建函数 `A` 的同时, 浏览器会在内存中创建一个对象 `B`，`A` 函数默认会有一个 `prototype ` 属性。指向了对象 `B`( 即：`prototype` 的属性的值是对象 `B` )。
​    这个对象 `B` 就是函数 `A` 的原型对象，简称函数的原型。
​    原型对象 `B` 默认会有一个属性 `constructor`  指向了函数 `A`  (即 `constructor`属性的值是函数 `A` )。
​    原型对象默认只有属性`constructor` 。其他都是从 `Object` 继承而来。

![](E:\notes\Pictures\JavaScript\JavaScript的原型对象的彻底理解\原型对象_01.png)

正式开始： 举栗子讨论

```js
//创建一个构造函数 Foo()，并用 new 关键字实例化该构造函数得到一个实例化对象 f1。
function Foo() {...};
let f1 = new Foo();
```

![](E:\notes\Pictures\JavaScript\JavaScript的原型对象的彻底理解\原型对象_02.png)


####  二、`__proto__` 属性

`  __proto__`属性，它是**对象所独有的**，可以看到`__proto__`属性都是由**一个对象指向一个对象**，即指向它们的原型对象（也可以理解为父对象），那么这个属性的作用是什么呢？

  它的**作用**就是当访问一个对象的属性时，如果该对象内部不存在这个属性，那么就会去它的`__proto__`属性所指向的那个对象（可以理解为父对象）里找，如果父对象也不存在这个属性，则继续往父对象的`__proto__`属性所指向的那个对象（可以理解为爷爷对象）里找，如果还没找到，则继续往上找….直到原型链顶端**null**。

  此时若还没找到，则返回`undefined`。以上这种通过`__proto__`属性来连接对象直到`null`的一条链即为我们所谓的**原型链**。

#### 三、`prototype` 属性

`prototype`是**函数所独有的**，它是从**一个函数指向一个对象**。

它的含义是**函数的原型对象**，也就是这个函数所创建的实例的原型对象，由此可知：

`f1.__proto__ === Foo.prototype`

`prototype`属性的**作用**：

  它的**作用**就是包含可以由特定类型的所有实例共享的属性和方法，也就是让该函数所实例化的对象们都可以找到公用的属性和方法。

#### 四、`constructor`属性

**constructor**属性也是**对象才拥有的**，它是从**一个对象指向一个函数**，含义就是**指向该对象的构造函数**，每个对象都有构造函数，从图中可以看出`**Function**` 这个对象比较特殊，它的构造函数就是它自己（因为 `Function` 可以看成是一个函数，也可以是一个对象），所有函数最终都是由 `Function()` 构造函数得来，所以**constructor**属性的终点就是**Function()**。

**举例子**

```js
//创建构造函数
function Person () { }

//使用Person.prototype 直接访问到原型对象
//给Person函数的原型对象中添加一个属性name，值是 "张三"
    Person.prototype.name = "张三";

//创建一个实例 p1
var p1 = new Person();
//访问p1对象的属性name，虽然在p1对象中我们并没有明确的添加属性name，但是p1的 prototype 属性指向的原型中有name属性，所以这个地方可以访问到属性name值。
        alert(p1.name);  // 张三
var p2 = new Person();
        alert(p2.name);  // 张三  都是从原型中找到的，所以一样。
        alert(p1.name === p2.name);  // true

// 由于不能修改原型中的值，下面这种方法就直接在p1中添加了一个新的属性name，然后在p1中无法再访问到原型中的属性。
        p1.name = "李四";
        alert("p1：" + p1.name);
// 对p2来说仍然是访问的原型中的属性。    
        alert("p2:" + p2.name);  // 张三  
//如何证明证明p1.__proto__ 与 Person.prototype是相同的
        alert(p1.__proto__ === Person.prototype);   //true
```

#### 五、常用方法

`hasOwnProperty()` 与 `in`操作符

作用：判断函数的原型所在位置

```js
function Person () {  };
Person.prototype.name = "志玲";
var p1 = new Person();
p1.sex = "女";

//定义一个函数去判断原型所在的位置
function propertyLocation(obj, prop){
    if(!(prop in obj)){
        alert(prop + "属性不存在");
    }else if(obj.hasOwnProperty(prop)){
        alert(prop + "属性存在于对象中");
    }else {
        alert(prop + "对象存在于原型中");
    }
}
propertyLocation(p1, "age");   //age属性不存在
propertyLocation(p1, "name");  //name对象存在于原型中
propertyLocation(p1, "sex");   //sex属性存在于对象中

```

#### 六、动态原型模式创建对象

```js
//构造方法内部封装属性
function Person(name, age) {
  //每个对象都添加自己的属性
  this.name = name;
  this.age = age;
  /*
      判断this.eat这个属性是不是function，如果不是function则证明是第一次创建对象，
      则把这个funcion添加到原型中。
      如果是function，则代表原型中已经有了这个方法，则不需要再添加。
      perfect！完美解决了性能和代码的封装问题。
  */
  if(typeof this.eat !== "function"){
      Person.prototype.eat = function () {
          alert(this.name + " 在吃");
      }
  }
}
var p1 = new Person("志玲", 40);
p1.eat(); //志玲 在吃
```
