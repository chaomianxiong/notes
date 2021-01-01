HTML 的 meta 标签

---

### 一、`name`  属性

`name` 属性:主要用于描述网页，比如网页的关键词，叙述等。与之对应的属性值为 `content`， `content`中的内容是对 `name` 填入类型的具体描述，便于搜索引擎抓取。

**语法：**

```html
<meta name="参数" content="具体的描述">。
<!--常用的有  keywords、description 、viewport -->
```


##### 1、 keywords

```html
<!--说明：用于告诉搜索引擎，你网页的关键字。举例：-->
<meta name="keywords" content="Lxxyx,博客，文科生，前端">
```

##### 2、 description(网站内容的描述)

```html
<!--说明：用于告诉搜索引擎，你网站的主要内容。举例：-->
<meta name="description" content="文科生，热爱前端与编程。目前大二，这是我的前端博客">
```

##### 3、viewport(移动端的窗口)

```html
<!-- 说明：这个概念较为复杂，具体的会在下篇博文中讲述。这个属性常用于设计移动端网页。在用bootstrap,AmazeUI等框架时候都有用过viewport。 -->
<meta name="viewport" content="width=device-width, initial-scale=1">
```

##### 4、其它参数

```html
4、robots(定义搜索引擎爬虫的索引方式)
 说明：robots用来告诉爬虫哪些页面需要索引，哪些页面不需要索引。content的参数有all,none,index,noindex,follow,nofollow。默认是all。
<meta name="robots" content="none">
具体参数如下：
1.none : 搜索引擎将忽略此网页，等价于noindex，nofollow。
2.noindex : 搜索引擎不索引此网页。
3.nofollow: 搜索引擎不继续通过此网页的链接索引搜索其它的网页。
4.all : 搜索引擎将索引此网页与继续通过此网页的链接索引，等价于index，follow。
5.index : 搜索引擎索引此网页。
6.follow : 搜索引擎继续通过此网页的链接索引搜索其它的网页。

5、author(作者)
<!--  -->
说明：用于标注网页作者举例：
<meta name="author" content="Lxxyx,841380530@qq.com">

6、 generator(网页制作软件)
说明：用于标明网页是什么软件做的举例: (不知道能不能这样写)：

<meta name="generator" content="Sublime Text3">
7、 copyright(版权)

说明：用于标注版权信息举例：

<meta name="copyright" content="Lxxyx"> //代表该网站为Lxxyx个人版权所有。
8、 revisit-after(搜索引擎爬虫重访时间)

说明：如果页面不是经常更新，为了减轻搜索引擎爬虫对服务器带来的压力，可以设置一个爬虫的重访时间。如果重访时间过短，爬虫将按它们定义的默认时间来访问。举例：

<meta name="revisit-after" content="7 days" >
9、 renderer(双核浏览器渲染方式)

说明：renderer是为双核浏览器准备的，用于指定双核浏览器默认以何种方式渲染页面。比如说360浏览器。举例：

<meta name="renderer" content="webkit"> //默认webkit内核
<meta name="renderer" content="ie-comp"> //默认IE兼容模式
<meta name="renderer" content="ie-stand"> //默认IE标准模式
```

### 二、http-equiv 属性

`http-equiv `顾名思义，相当于 `http` 的文件头作用。相当于 `HTTP` 的作用，比如说定义些 `HTTP` 参数啥的。

**语法：**

```html
<meta http-equiv="参数" content="具体的描述">
```

##### 具体参数

```html
1、 content-Type(设定网页字符集)(推荐使用HTML5的方式)
   说明：用于设定网页字符集，便于浏览器解析与渲染页面举例：
<meta http-equiv="content-Type" content="text/html;charset=utf-8"> //旧的HTML，不推荐
<meta charset="utf-8"> //HTML5设定网页字符集的方式，推荐使用UTF-8

2、 X-UA-Compatible(浏览器采取何种版本渲染当前页面)
   说明：用于告知浏览器以何种版本来渲染页面。（一般都设置为最新模式，在各大框架中这个设置也很常见。）举例：
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/> //指定IE和Chrome使用最新版本渲染当前页面

3、cache-control(指定请求和响应遵循的缓存机制)用法1.
   说明：指导浏览器如何缓存某个响应以及缓存多长时间。这一段内容我在网上找了很久，但都没有找到满意的。最后终于在Google Developers中发现了我想要的答案。
   移动开发常用head，meta标签
举例:
<meta http-equiv="cache-control" content="no-cache">
共有以下几种用法：
no-cache: 先发送请求，与服务器确认该资源是否被更改，如果未被更改，则使用缓存。
no-store: 不允许缓存，每次都要去服务器上，下载完整的响应。（安全措施）
public : 缓存所有响应，但并非必须。因为max-age也可以做到相同效果
private : 只为单个用户缓存，因此不允许任何中继进行缓存。（比如说CDN就不允许缓存private的响应）
maxage : 表示当前请求开始，该响应在多久内能被缓存和重用，而不去服务器重新请求。例如：max-age=60表示响应可以再缓存和重用 60 秒。

用法2.(禁止百度自动转码)
   说明：用于禁止当前页面在移动端浏览时，被百度自动转码。虽然百度的本意是好的，但是转码效果很多时候却不尽人意。所以可以在head中加入例子中的那句话，就可以避免百度自动转码了。举例：
<meta http-equiv="Cache-Control" content="no-siteapp" />

4、expires(网页到期时间)
   说明:用于设定网页的到期时间，过期后网页必须到服务器上重新传输。举例：
<meta http-equiv="expires" content="Sunday 26 October 2016 01:00 GMT" />

5、refresh(自动刷新并指向某页面)
   说明：网页将在设定的时间内，自动刷新并调向设定的网址。举例:
<meta http-equiv="refresh" content="2；URL=http://www.lxxyx.win/"> //意思是2秒后跳转向我的博客

6、Set-Cookie(cookie设定)
   说明：如果网页过期。那么这个网页存在本地的cookies也会被自动删除。
<meta http-equiv="Set-Cookie" content="name, date"> //格式
<meta http-equiv="Set-Cookie" content="User=Lxxyx; path=/; expires=Sunday, 10-Jan-16 10:00:00 GMT"> 
```

### 三、`name` 属性的 `viewport` 参数

```html
经常这样写：
<meta name ="viewport" content ="width=device-width, initial-scale=1, maximum-scale=3, minimum-scale=1, user-scalable=no">

content参数：
width viewport 宽度(数值/device-width)
height viewport 高度(数值/device-height)
initial-scale 初始缩放比例
maximum-scale 最大缩放比例
minimum-scale 最小缩放比例
user-scalable 是否允许用户缩放(yes/no)
iPhone 6 和 iPhone 6+ ：
<meta name="viewport" content="width=375">
<meta name="viewport" content="width=414">
```

#### 1、 `ios` 设备的设置

```html
iOS设备

添加到主屏后的标题
<meta name="apple-mobile-web-app-title" content="标题">是否启用webAPP进入全屏模式
<meta name="apple-mobile-web-app-capable" content="yes" />状态栏的背景颜色
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
content参数default 默认值。
black 状态栏背景是黑色。
black-translucent 状态栏背景是黑色半透明。
如果设置为 default 或 black ,网页内容从状态栏底部开始。
如果设置为 black-translucent ,网页内容充满整个屏幕，顶部会被状态栏遮挡。
禁止数字识别为电话号码
<meta name="format-detection" content="telephone=no" />
iOS图标

link标签，rel 参数： apple-touch-icon 图片自动处理成圆角和高光等效果。

apple-touch-icon-precomposed 禁止系统自动添加效果，直接显示设计原图。

iPhone 和 iPod touch，默认 57×57px
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png" />iPad，72×72px
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="/apple-touch-icon-72x72-precomposed.png" />Retina iPhone 114×114px
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="/apple-touch-icon-114x114-precomposed.png" />Retina iPad，144×144px
<link rel="apple-touch-icon-precomposed" sizes="144x144" href="/apple-touch-icon-144x144-precomposed.png" />iOS 图标大小在iPhone 6+上是180×180，iPhone 6 是120×120
适配iPhone 6+ <link rel="apple-touch-icon-precomposed" sizes="180x180" href="retinahd_icon.png">
iOS 启动画面

Apple的文档 链接

iPad启动画面不包括状态栏区域

iPad竖屏 768x1004
<link rel="apple-touch-startup-image" sizes="768x1004" href="/splash-screen-768x1004.png" />iPad 竖屏 1536×2008（Retina）iPad 横屏 1024×748（标准分辨率）iPad 横屏 2048×1496（Retina）
iPhone 和 iPod touch 的启动画面是包含状态栏区域的

iPhone/iPod Touch 竖屏 320×480 (标准分辨率)
<link rel="apple-touch-startup-image" href="/splash-screen-320x480.png" />
iPhone/iPod Touch 竖屏 640×960 (Retina)iPhone 5/iPod Touch 5 竖屏 640×1136 (Retina)iPhone 6对应的图片大小是750×1294，iPhone 6 Plus 对应的是1242×2148 。
<link rel="apple-touch-startup-image" href="launch6.png" media="(device-width: 375px)">
<link rel="apple-touch-startup-image" href="launch6plus.png" media="(device-width: 414px)">添加智能 App 广告条 Smart App Banner（iOS 6+ Safari）
<meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">、
```

#### 2、其它设备设置

```html
Android
  Android Lollipop 中的 Chrome 39 增加 theme-color meta 标签，用来控制选项卡颜色。
移动开发常用head，meta标签
<meta name="theme-color" content="#db5945">

Win 8
Windows 8 磁贴颜色
<meta name="msapplication-TileColor" content="#000"/>Windows 8 磁贴图标
<meta name="msapplication-TileImage" content="icon.png"/>

RSS
添加RSS订阅
<link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml" />
```

### 四、`meta` 的基本范例

```html
<!DOCTYPE html> <!-- 使用 HTML5 doctype，不区分大小写 -->
<html lang="zh-cmn-Hans"> <!-- 更加标准的 lang 属性写法 http://zhi.hu/XyIa -->
<head>
 <!-- 声明文档使用的字符编码 -->
 <meta charset='utf-8'>
 <!-- 优先使用 IE 最新版本和 Chrome -->
 <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>
 <!-- 页面描述 -->
 <meta name="description" content="不超过150个字符"/>
 <!-- 页面关键词 -->
 <meta name="keywords" content=""/>
 <!-- 网页作者 -->
 <meta name="author" content="name, email@gmail.com"/>
 <!-- 搜索引擎抓取 -->
 <meta name="robots" content="index,follow"/>
 <!-- 为移动设备添加 viewport -->
 <meta name="viewport" content="initial-scale=1, maximum-scale=3, minimum-scale=1, user-scalable=no">
 <!-- width=device-width 会导致 iPhone 5 添加到主屏后以 WebApp 全屏模式打开页面时出现黑边 http://bigc.at/ios-webapp-viewport-meta.orz -->
 <!-- iOS 设备 begin -->
 <meta name="apple-mobile-web-app-title" content="标题">
 <!-- 添加到主屏后的标题（iOS 6 新增） -->
 <meta name="apple-mobile-web-app-capable" content="yes"/>
 <!-- 是否启用 WebApp 全屏模式，删除苹果默认的工具栏和菜单栏 -->
 <meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">
 <!-- 添加智能 App 广告条 Smart App Banner（iOS 6+ Safari） -->
 <meta name="apple-mobile-web-app-status-bar-style" content="black"/>
 <!-- 设置苹果工具栏颜色 -->
 <meta name="format-detection" content="telphone=no, email=no"/>
 <!-- 忽略页面中的数字识别为电话，忽略email识别 -->
 <!-- 启用360浏览器的极速模式(webkit) -->
 <meta name="renderer" content="webkit">
 <!-- 避免IE使用兼容模式 -->
 <meta http-equiv="X-UA-Compatible" content="IE=edge">
 <!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
 <meta name="HandheldFriendly" content="true">
 <!-- 微软的老式浏览器 -->
 <meta name="MobileOptimized" content="320">
 <!-- uc强制竖屏 -->
 <meta name="screen-orientation" content="portrait">
 <!-- QQ强制竖屏 -->
 <meta name="x5-orientation" content="portrait">
 <!-- UC强制全屏 -->
 <meta name="full-screen" content="yes">
 <!-- QQ强制全屏 -->
 <meta name="x5-fullscreen" content="true">
 <!-- UC应用模式 -->
 <meta name="browsermode" content="application">
 <!-- QQ应用模式 -->
 <meta name="x5-page-mode" content="app">
 <!-- windows phone 点击无高光 -->
 <meta name="msapplication-tap-highlight" content="no">
 <!-- iOS 图标 begin -->
 <link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png"/>
 <!-- iPhone 和 iTouch，默认 57x57 像素，必须有 -->
 <link rel="apple-touch-icon-precomposed" sizes="114x114" href="/apple-touch-icon-114x114-precomposed.png"/>
 <!-- Retina iPhone 和 Retina iTouch，114x114 像素，可以没有，但推荐有 -->
 <link rel="apple-touch-icon-precomposed" sizes="144x144" href="/apple-touch-icon-144x144-precomposed.png"/>
 <!-- Retina iPad，144x144 像素，可以没有，但推荐有 -->
 <!-- iOS 图标 end -->
 <!-- iOS 启动画面 begin -->
 <link rel="apple-touch-startup-image" sizes="768x1004" href="/splash-screen-768x1004.png"/>
 <!-- iPad 竖屏 768 x 1004（标准分辨率） -->
 <link rel="apple-touch-startup-image" sizes="1536x2008" href="/splash-screen-1536x2008.png"/>
 <!-- iPad 竖屏 1536x2008（Retina） -->
 <link rel="apple-touch-startup-image" sizes="1024x748" href="/Default-Portrait-1024x748.png"/>
 <!-- iPad 横屏 1024x748（标准分辨率） -->
 <link rel="apple-touch-startup-image" sizes="2048x1496" href="/splash-screen-2048x1496.png"/>
 <!-- iPad 横屏 2048x1496（Retina） -->
 <link rel="apple-touch-startup-image" href="/splash-screen-320x480.png"/>
 <!-- iPhone/iPod Touch 竖屏 320x480 (标准分辨率) -->
 <link rel="apple-touch-startup-image" sizes="640x960" href="/splash-screen-640x960.png"/>
 <!-- iPhone/iPod Touch 竖屏 640x960 (Retina) -->
 <link rel="apple-touch-startup-image" sizes="640x1136" href="/splash-screen-640x1136.png"/>
 <!-- iPhone 5/iPod Touch 5 竖屏 640x1136 (Retina) -->
 <!-- iOS 启动画面 end -->
 <!-- iOS 设备 end -->
 <meta name="msapplication-TileColor" content="#000"/>
 <!-- Windows 8 磁贴颜色 -->
 <meta name="msapplication-TileImage" content="icon.png"/>
 <!-- Windows 8 磁贴图标 -->
 <link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml"/>
 <!-- 添加 RSS 订阅 -->
 <link rel="shortcut icon" type="image/ico" href="/favicon.ico"/>
 <!-- 添加 favicon icon -->
 <title>标题</title>
</head>
这是一个基本范例
</body>
```

