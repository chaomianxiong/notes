```js
btn.onclick = function () {

  let data = {};
  //1、创建 ajax 对象
  let xhr = new XHRHttpRequest();
  //2、链接到服务器
  xhr.open('post', 'http://127.0.0.1:8000/aside.json', true)
//发送请求
xhr.send(JSON.stringify({
  username: '炒面熊',
  pwd: '123456'
}));
//接收返回值
  xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && /^2\d{2}/.test(xhr.status)) {
      console.log(xhr.responseText);
      result.innerHTML = xhr.response;
    }
  }

  
}
```

axios

创建实例

请求拦截

响应拦截

如何引用

一、第三方的往前靠

二、自己的往后靠

1、jsx往前靠

2、图片往后靠

