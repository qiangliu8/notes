# Ajax

[TOC]



## 一、原生Ajax

### 1.1 Ajax简介

Ajax全称是异步的JS和XML

通过AJAX可以在浏览器中向服务器发送异步请求，最大的优势:**无刷新获取数据**。

AJAX不是新的编程语言，而是一种将现有的标准组合在一起使用的新方式。

### 1.2 XML简介

XML可扩展标记语言

XML被用来传输和存储数据

XML和HTML类似，不同的是HTML中都是预定义标签，而XML中没有预定义标签，全都是自定义标签，用来表示一些数据。

![1644399569533](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1644399569533.png)

![1644399678642](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1644399678642.png)

### 1.3 Ajax的特点

#### 1.3.1优点

1. 可以无需刷新页面而与服务器端进行通信
2. 允许你根据用户时间来更新部分页面内容

#### 1.3.2缺点

1. 没有浏览历史，不能回退
2. 存在跨域问题
3. SEO不友好

### 1.4 Ajax的使用

#### 1.4.1Ajax发送请求

```js
//1.创建对象
const xhr = new XMLHttpRequest();
//2. 初始化 设置请求方法和url
xhr.open('GET', 'http://localhost:8000/server?name=123');
//3.发送
xhr.send();
//4.事件绑定 处理服务端返回的结果
//readystate标识状态 0 1 2 3 4
xhr.onreadystatechange = function() {
    //判断（服务端返回了所有的结果）
    if (xhr.readyState == 4) {
        if (xhr.status >= 20 && xhr.status < 300) {
            console.log(xhr.status) //状态码
            console.log(xhr.statusText) //状态字符串
            console.log(xhr.getAllResponseHeaders()) //所有响应头
            console.log(xhr.response) //响应体
        }
    }
}
```

访问结果

![1644500961256](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1644500961256.png)

#### 1.4.2Ajax发送post请求

服务端添加post路由

```js
app.post('/server1', (request, response) => {
    //设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    //设置响应体
    response.send('hello ajax1')
});
```

前端发送请求

```js
//1.创建对象
const xhr = new XMLHttpRequest()
//2. 初始化 设置请求方法和url
xhr.open('POST', 'http://localhost:8000/server1')
//3.发送
xhr.send()
//4.事件绑定 处理服务端返回的结果
//readystate标识状态 0 1 2 3 4
xhr.onreadystatechange = function() {
    if (xhr.readyState == 4) {
        if (xhr.status >= 200 & xhr.status < 300) {
        }
    }
}
```

前端发送**带参数**的请求

```js
xhr.send('name=liuqiang&age=24')
```

#### 1.4.3设置请求头信息

前端设置发送请求的

```js
xhr.setRequestHeader('content-type', 'application/x-www-form-urlencoded')
```

后端设置可以接收的请求头

```js
//设置响应头 设置允许跨域
response.setHeader('Access-Control-Allow-Origin', '*');
//设置响应体
response.setHeader('Access-Control-Allow-Headers','*')
```

后端接收任意的请求 不管post还是get

```js
app.all('/server1', (request, response) => {
    //设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    //设置响应体
    response.setHeader('Access-Control-Allow-Headers', '*')
        //设置响应体
    response.send('hello ajax1')
});
这样就可以接收前端设置自定义的请求体
```

![1644504180856](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1644504180856.png)

#### 1.4.4服务端响应json数据

**1.后端返回json**

```js
app.all('/json', (request, response) => {
    //设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    //设置响应体
    const data = {
        name: '这是后端返回的json'
    }
    let str = JSON.stringify(data)
    response.send(str)
});
```

**2.前端获取 解析json**

```JS
//1.创建对象
const xhr = new XMLHttpRequest()
//2. 初始化 设置请求方法和url
xhr.open('POST', 'http://localhost:8000/json')
//3.发送
xhr.send()
//4.事件绑定 处理服务端返回的结果
xhr.onreadystatechange = function() {
    if (xhr.readyState == 4) {
        if (xhr.status >= 200 & xhr.status < 300) {
            let data = JSON.parse(xhr.responseText)
            div.innerHTML = data.name
        }
    }
}
```

**或者前端自动转换json**

```js

//设置响应体返回的是json格式
xhr.responseType = 'json'

.......

div.innerHTML = xhr.response.name

```

#### 1.4.5清除ie缓存

前端请求时带上时间戳 

```js
xhr.open('POST', 'http://localhost:8000/json?date=' + Date.now())
```

#### 1.4.6请求超时与网络异常处理

前端设置超时设置

```js
//1.创建对象
const xhr = new XMLHttpRequest()
//2. 初始化 设置请求方法和ur
xhr.open('POST', 'http://localhost:8000/time')
//设置超时限制2s
xhr.timeout = 2000
//设置超时回调
xhr.ontimeout = function() {
    alert('请求异常，请稍后')
}
//设置网络异常回调
xhr.onerror =function(){
    alert('网络异常，请稍后')
}
//3.发送
xhr.send()
//4.事件绑定 处理服务端返回的结果
xhr.onreadystatechange = function() {
    if (xhr.readyState == 4) {
        if (xhr.status >= 200 & xhr.status < 300) {
        }
    }
}
```

后端设置延迟发送

```js
app.all('/time', (request, response) => {
    response.setHeader('Access-Control-Allow-Origin', '*');
    setTimeout(function() {
        response.send('延时响应')
    }, 3000)
});
```

设置超时回调

```js
xhr.ontimeout = function() {
    alert('请求异常，请稍后')
}
```

设置网络异常回调

```js
xhr.onerror =function(){
    alert('网络异常，请稍后')
}
```

#### 1.4.7取消请求

```js
let xhr = null
//移入发送
div.addEventListener('mouseover', function() {
    //1.创建对象
    xhr = new XMLHttpRequest()
    //2. 初始化 设置请求方法和url
    xhr.open('get', 'http://localhost:8000/abort')
    //3.发送
    xhr.send()
})
//移出取消
div.addEventListener('mouseout', function() {
    xhr.abort()
})
```

<img src="C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1644914960798.png" alt="1644914960798" style="zoom: 200%;" />

#### 1.4.8 请求重复发送问题

```js
let xhr = null
let isSending = false //表示变量的值
div.addEventListener('mouseover', function() {
    if (isSending) xhr.abort()
    //1.创建对象
    const xhr = new XMLHttpRequest()
    //2. 初始化 设置请求方法和url
    isSending = true
    xhr.open('POST', 'http://localhost:8000/cancel')
    //3.发送
    xhr.send('name=liuqiang&age=24')
    //4.事件绑定 处理服务端返回的结果
    xhr.onreadystatechange = function() {
        if (xhr.readyState == 4) {
            isSending = false
        }
    }
})
```

## 二、jQuery发送ajax请求

### 2.1常用jq

```js
$.get('http://localhost:8000/jq', {
    a: 10,
    b: 100
}, function(data) {
    console.log(data)
})


//返回解析为json对象
$.post('http://localhost:8000/jq', {
    a: 10,
    b: 100
}, function(data) {
    console.log(data)
}, 'json')
```

### 2.2通用方法发送jq

```js
$.ajax({
    url: 'http://localhost:8000/jq',
    data: {
        a: 100,
        b: 10086
    },
    type: 'GET',
    dataType: 'json',
    timeout: 2000,
    success: function(data) {
        console.log(data)
    },
    error: function() {
        console.log('出错了')
    },
    //头信息
    headers: {
        d: 300
    }
})
```

## 三、Axios发送请求

```js
axios.defaults.baseURL = 'http://localhost:8000'
axios.post('/axios', {
    height: 180,
    weight: 180
}, {
    //url参数
    params: {
        id: 100,
        name: 'liuqiang'
    },
    //请求头参数
    headers: {
        name: 'liuqiang',
        age: 24
    },
    //请求体

}).then(value => {
    console.log(value)
})
```

axios函数发送请求

```js
axios({
    url: '/axios',
    //url参数
    params: {
        id: 100,
        name: 'liuqiang'
    },
    //请求头参数
    headers: {
        name: 'liuqiang',
        age: 24
    },
    //请求头参数
    headers: {
        name: 'liuqiang',
        age: 24
    },
    //请求体
    data: {
        height: 180,
        weight: 180
    }
}).then(response=>{
    console.log(response)
    console.log(response.status)
    console.log(response.statusText)
    console.log(response.headers)
    console.log(response.data)
})
```

## 四、fetch函数发送ajax请求

```js
fetch('http://localhost:8000/fetch-server', {
    //请求方法
    method: 'POST',
    //请求头
    headers: {
        name: 'liuqiang'
    },
    //请求体
    body: 'name=liuqiang'
}).then(response => {
    return response.text()
}).then(response => {
    console.log(response)
})
```

## 五、跨域

同源策略是最早有Netscape公司提出的一种浏览器的安全策略。

**同源：协议、域名、端口号、必须完全相同**

违背同源策略就是跨域

1. 后台跳转前台页面

   ```js
   app.all('/home', (request, response) => {
       response.sendFile(__dirname + '/index.html')
   });
   ```

2. 前端页面发送的请求就不需要带上地址 默认带上服务器的地址，这就是同源

   ```js
   xhr.open('GET', '/server?name=123');
   ```

### 5.2如何解决跨域

#### 5.2.1 Jsonp

Jsonp是以非官方的跨域解决方案，**只支持get请求**

jsonp就是利用script标签的跨域能力来发送请求的。

##### Jsonp的使用

1. 后端写服务 调用前端的函数

   ```js
   app.all('/script', (request, response) => {
       response.setHeader('Access-Control-Allow-Origin', '*');
       //设置响应体
       response.setHeader('Access-Control-Allow-Headers', '*')
       let data = {
           name: '刘强'
       }
       let Str = JSON.stringify(data)
       response.send(`handle(${Str})`)
   });
   ```

2. 前端通过script标签 调用这个服务

   ```js
   <script>
       function handle(data) {
           console.log(data.name)
       }
   </script>
   <script src="http://localhost:8000/script"></script>
   ```

##### 

#### 5.2.2 CROS

CROS (Cross-Origin Resource Sharing)，跨域资源共享。CORS是官方的跨域解决方案，它的特点是不需要在客户端做任何特殊的操作，完全在服务器中进行处理，支持get和 post请求。跨域资源共享标准新增了一组HTTP首部字段，允许服务器声明哪些源站通过浏览器有权限访问哪些资源

CROS怎么工作的?

CORS是通过设置一个响应头来告诉浏览器，该请求允许跨域，浏览器收到该响应以后就会对响应放行。

主要是服务器端的设置:

```js
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*')
    response.setHeader('Access-Control-Allow-Method', '*')
```



## HTTP

#### 概念

HTTP（hypertext transport protocol）协议【超文本传输协议】。协议详细规定了浏览器和万维网服务器之间互相通信的规则。

#### 请求报文

重点是格式与参数

**行** GET /s?ie=utf-8 HTTP/1.1

**头**![1644400706704](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1644400706704.png)

**空行**

**体** 如果是get 请求体是空的 如果是post带上参数 

#### 响应报文

**行** HTTP/1.1 200  OK

**头**![1644400927922](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1644400927922.png)

**空行**

**体** ![1644400947682](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1644400947682.png)

## Express

**1.安装express命令，自动安装依赖包**

```
npm i express
```

![1644500691542](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1644500691542.png)

**2.配置express文件  index.js** 

```javascript
//1.引入express
const express = require('express');
//2.创建应用对象
const app = express();
//3.创建路由规则
//request是对请求报文的封装 response是对响应报文的封装
app.get('/server', (request, response) => {
    //设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    //设置响应体
    response.send('hello ajax')
});

//4.监听端口启动服务
app.listen(8000, () => {
    console.log('服务已经启动，8000端口监听中')
})
```

**3.启动服务**

```js
node index.js
服务已经启动，8000端口监听中
```

**4.访问端口**

访问 http://localhost:8000/server

**5.启动nodemon**

```js
npm install -g nodemon
```

启动服务 不是node 而改为nodemon

```js
npx nodemon server.js
```

自动刷新无需手动启动