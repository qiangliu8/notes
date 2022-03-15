# axios从0开始

[TOC]

## 一、JSON_Server

1.安装json-server

```js
npm install -g json-server
```

2.创建json文件存数据

```json
{
    "posts": [
        { "id": 1, "title": "json-server", "author": "typicode" },
        { "id": 2, "name": "刘强", "author": "typicode" }
    ],
    "comments": [
        { "id": 1, "body": "some comment", "postId": 1 }
    ],
    "profile": { "name": "typicode" }
}
```

3.开启json服务

```js
json-server --watch db.json
```

![1646192042532](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646192042532.png)

Now if you go to [http://localhost:3000/posts/2](http://localhost:3000/posts/1), you'll get

```
 "id": 2, "name": "刘强", "author": "typicode" }
```

##  二、axios 的理解和使用 

### 2.1 axios是什么

1. 前端最流行的ajax请求库
2.  react/vue 官方都推荐使用 axios 发 ajax 请求  
3.   文档: https://github.com/axios/axios 

### 2.2 axios特点

- 基于xhr+promise的异步ajax请求
- 浏览器端/node端都可以使用
- 支持请求/响应拦截器
- 支持请求取消
- 请求/响应数据转换
- 批量发送多个请求

### 2.3 axios基本使用

 **axios(config): 通用/最本质的发任意类型请求的方式** 

```js
//查询数据
$('#get').click(() => {
    //查看
    axios({
        method: 'get',
        url: 'http://localhost:3000/posts/2',
    }).then(response => {
        console.log(response)
    })

})

//添加数据
$('#post').click(() => {
    //添加新的文章
    axios({
        method: 'post',
        url: 'http://localhost:3000/posts',
        //设置请求体
        data: {
            title: '云边的小卖铺',
            author: '俞文竹'
        }
    }).then(response => {
        console.log(response)
    })

})

//更新数据
$('#put').click(() => {
    //修改的文章
    axios({
        method: 'put',
        url: `http://localhost:3000/posts/1`,
        //设置请求体
        data: {
            title: '三国演义',
            author: '刘强'
        }
    }).then(response => {
        console.log(response)
    })

})


//删除数据
$('#delete').click(() => {
    //删除文章
    axios({
        method: 'delete',
        url: `http://localhost:3000/posts/3`,
        //不用设置请求体
    }).then(response => {
        console.log(response)
    })

})
```

### 2.4 axios其他方式发送请求

 **axios.request(config): 等同于 axios(config)**  

```js
axios.request({
    method: 'get',
    url: 'http://localhost:3000/comments'
}).then(response => {
    console.log(response)
})
```

 **axios.post(url[, data, config]): 发 post 请求**  

```js
axios.post(
    'http://localhost:3000/comments', {
        "body": "奶奶常说！",
        "postId": 2
    }).then(response => {
    console.log(response)
})
```

**axios.get(url[, config]): 发 get 请求** 

**axios.delete(url[, config]): 发 delete 请求**   

**axios.put(url[, data, config]): 发 put 请求** 

![1646210746778](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646210746778.png)

### 2.5请求响应的结构

 { data, status, statusText, headers, config, request }  

### 2.6 默认配置

**axios.defaults.xxx:请求的默认全局配置**

```js
axios.defaults.method = 'get' //设置默认请求的类型
axios.defaults.baseURL = 'http://localhost:3000' //设置基础url
axios.defaults.params = { id: 1 }
axios.defaults.timeout = 3000

axios({
    url: '/posts'
}).then(res => {
    console.log(res)
})

//Request URL: http://localhost:3000/posts?id=1
```

### 2.7 创建实例对象发送请求

 **axios.create(config)** 

例化对象和axios对象的功能几乎是一样的

```js
const obj = axios.create({
    baseURL: 'http://localhost:3000',
    timeout: 2000
})

console.log(obj) //ƒ (){for(var n=new Array(arguments.length),r=0;r<n.length;r++)n[r]=arguments[r];return e.apply(t,n)}

obj({
    url: '/profile'
}).then(res => {
    console.log(res)
})

//也可以调用axios的方法
obj.get('/profile').then(res => {
    console.log(res.data)
})
```

实例不同的对象，每个对象访问不同的域名。简而言之就是， **根据指定配置创建一个新的 axios, 也就就每个新 axios 都有自己的配置**。

 需求: 项目中有部分接口需要的配置与另一部分接口需要的配置不太一 样, 如何处理 ？

 解决: 创建 2 个新 axios, 每个都有自己特有的配置, 分别应用到不同要 求的接口请求中  

### 2.8 axios拦截器

基本使用

```js
//设置请求拦截器
axios.interceptors.request.use(function(config) {
    console.log('请求拦截器')
    throw '请求拦截器跑一个错'
    return config
}, function(err) {
    console.log('请求拦截器 失败')
    return Promise.reject(err)
})

//设置响应拦截器
axios.interceptors.response.use(function(response) {
    console.log('响应拦截器')
    return response
}, function(err) {
    console.log('响应拦截器 失败')
    return Promise.reject(err)
})

//发送请求
axios({
    method: 'get',
    url: 'http://localhost:3000/posts'
}).then(res => {
    console.log('奥里给！')
}).catch(err => {
    console.log(err)
})
```

 修改拦截器中的config参数和response参数                                                             

```js
//设置请求拦截器
axios.interceptors.request.use(function(config) {
    //修改config参数
    config.params = { id: 1 }
    return config
}, function(err) {
    console.log('请求拦截器 失败')
    return Promise.reject(err)
})

//设置响应拦截器
axios.interceptors.response.use(function(response) {
    //处理拦截器中的响应体
    return response.data
}, function(err) {
    console.log('响应拦截器 失败')
    return Promise.reject(err)
})
```

说明：调用axios()并不是立即发送ajax请求，而是经历较长的流程。！！

**流程：请求拦截器2=》请求拦截器2=》发送ajax请求=》响应拦截器1=》响应拦截器2=》请求的回调**

注意：此流程是通过promise串联起来的，**请求拦截器传递的是config**，**响应拦截器传递的是response**

### 2.9 axios取消请求

先把后端请求延迟设置2s

```js
json-server --watch db.json -d 2000
```

```js
//1.设置全局变量
let cancel = null
//查询数据
$('#send').click(() => {
    axios({
        method: 'get',
        url: 'http://localhost:3000/posts/2',
        //2.添加配置对象的属性
        cancelToken: new axios.CancelToken(c => {
            //3.将c的值赋值给cancel
            cancel = c
        })
    }).then(response => {
        console.log(response)
    })

})

//添加数据
$('#cancel').click(() => {
    //4.执行取消函数
    cancel()

})
```

添加防抖 取消重复点击

```js
//1.设置全局变量
let cancel = null
    //查询数据
$('#send').click(() => {
    //检查上上一次请求是否已经完成
    if (cancel != null) {
        cancel()
    }
    axios({
        method: 'get',
        url: 'http://localhost:3000/posts/2',
        //2.添加配置对象的属性
        cancelToken: new axios.CancelToken(c => {
            //3.将c的值赋值给cancel
            cancel = c
        })
    }).then(response => {
        cancel = null
        console.log(response)
    })

})
//添加数据
$('#cancel').click(() => {
    cancel()
})
```

## 三、axios源码解析

### 3.1 源码目录结构

![1646226659613](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646226659613.png)

### 3.2 源码分析总结

#### 3.2.1 axios和Axios的关系

- 从语法上来看：axios不是Axios的实例
- 从功能上来说：axios是Axios的实例
- **axios是Axios.prototype.request函数bind()返回的函数**
- **axios作为对象有Axios原型对象上的所有方法，有Axios对象上所有属性**

#### 3.2.2 instance与axios的区别

相同

1. 都是一个能发任意请求的函数：request(config)
2. 都有发特定请求的各种方法：get()/post()/put()/delete() 
3. 都有默认配置和拦截器的属性:defaults/interceptors

不同

1. 默认配置很不一样
2. instance没有axios后面添加的一些方法：creat()/CancelToken()/all

#### 3.2.3 axios运行的整体流程

![1646378886270](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646378886270.png)

1. 整体流程

   **request(config) =>dispatchRequest(config)=>xhrAdapter(config)**

2. reqest(config)

   将请求拦截器/dispactchRequest()/响应拦截器 **通过promise链串联起来**

3. dispatchRequest(config)

   转换请求数据=>调用xhrAdapter()发请求=>请求返回后转换响应数据，返回promise

4. xhrAdapter(config)

   创建xhr对象，根据config进行相应设置，发送特定请求，并接收响应数据，返回promise

#### 3.2.4 axios的请求/响应拦截器是什么

![1646379361165](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646379361165.png)

1. **请求拦截器**

   在真正发送请求前执行的回调函数

   可以对请求进行检查或配置进行特定处理

   成功的回调函数，**传递的默认必须是config**

   失败的回调函数，传递的默认是error

2. **响应拦截器**

    在请求得到响应后执行的回调函数  

    可以对响应数据进行特定处理 

    成功的回调函数, 传递的默认是 response 

    失败的回调函数, 传递的默认是 error  

#### 3.2.5 axios的请求/响应数据转换器是什么

1. 请求转换器：对请求头和请求体数据进行特性处理的函数

   ```js
   if (utils.isObject(data)) {
       setContentTypeIfUnset(headers, 'application/json;charset=utf-8');
       return JSON.stringify(data);
   }
   ```

2. 响应转换器：将响应体json字符串解析为js对象或数组的函数

   ```js
   response.data = JSON.parse(response.data)
   ```

#### 3.2.6 response的整体结构 

```js
{
    data,
        status,
        statusText,
        headers,
        config,
        request
}
```

#### 3.2.7 error的整体结构 

```js
{
	message,
        response,
        request
}
```

#### 3.2.8 如何取消未完成的请求

1. 当配置了cancelToken对象时，保存cancel函数
   1. 创建一个用于将来中断请求的cancelPromise
   2. 并定义一个用于取消请求的cancel函数
   3. 将cancel函数传递出来
2. 调用cancel()取消请求
   1. 执行canel函数，传入错误信息message
   2. 内部会让cancelPromise变为成功，且成功的值为一个Cancel对象
   3. 在cancelPromise的成功回调中中断请求，并让发请求的promise失败，失败的reason为Cancel对象

### 3.3 axios对象创建过程模拟实现

实际就是创建一个axios对象，在创建一个axios原型上的request函数，然后这个函数的使用是axios对象的指向。

```js
//构造函数
function Axios(config) {
    //初始化
    this.defaults = config //为了创建default默认属性
    this.interceptors = {
        request: {},
        response: {}
    }
}
//原型添加相关的方法
Axios.prototype.request = function(config) {
    console.log('发送ajax请求' + config.method)
}
Axios.prototype.get = function(config) {
    return this.request({
        method: 'get'
    })
    console.log('发送get请求')
}
Axios.prototype.post = function(config) {
    console.log('发送post请求')
    return this.request({
        method: 'post'
    })
}

//声明函数
function createInstance(config) {
    //实例化一个对象
    let context = new Axios(config) //可以使用 context.get() context.post() 但是因为是实例对象，所有不能使用context()
    //创建请求函数
    let instance = Axios.prototype.request.bind(context) //instances是一个函数，并且可以使用instance({}), 此时不能当对象用 即instance.get()
    //将Axios的prototype对象中的方法添加到instance函数对象中
    Object.keys(Axios.prototype).forEach(key => {
        instance[key] = Axios.prototype[key].bind(context)
    })
    //为instance函数对象添加属性 default与interceptors
    Object.keys(context).forEach(key => {
        instance[key] = context[key]
    })
    return instance
}

let axios = createInstance()

console.log(axios)
axios({method: 'get'})

axios.get({})
axios.request({method: 'get'})
```

### 3.4 axios发送请求

```js
//axios  等同于Axios.prototype.request   是通过bind的
//1.声明构造函数  
function Axios(config) {
    this.config = config
}

Axios.prototype.request = function(config) {
    //发送请求
    //创建一个promise对象
    let promise = Promise.resolve(config)
    //声明一个数组
    let chains = [dispatchRequest, undefined] //undefined占位
    //调用then方法
    let result = promise.then(chains[0], chains[1])
    return result
}


//2.dispatchRequest函数
function dispatchRequest(config) {
    //调用适配器发送请求
    return xhrAdapter(config).then(response => {
        console.log(response)
    }, error => {
        throw error
    })
}
//3。adapter函数
function xhrAdapter(config) {
    return new Promise((resolve, reject) => {
        let xhr = new XMLHttpRequest()
        xhr.open(config.method, config.url)
        xhr.send()
        xhr.onreadystatechange = () => {
            if (xhr.readyState == 4) {
                if (xhr.status >= 200 && xhr.status < 300) {
                    resolve({
                        config: config,
                        data: xhr.response,
                        headers: xhr.getResponseHeader,
                        request: xhr,
                        status: xhr.statusText
                    })
                } else {
                    reject('服务出错了!')
                }
            }
        }
    })
}

//4. 创建axios函数
let axios = Axios.prototype.request.bind(null)

axios({
    method: 'get',
    url: 'http://localhost:3000/posts'
}).then(res => {
    console.log(res)
}, rej => {
    console.log(rej)
})
```

### 3.5 实现拦截器

```js
//构造函数 
function Axios(config) {
    this.config = config
    this.interceptors = {
        request: new InterceptorsManagers(),
        response: new InterceptorsManagers(),
    }
}

Axios.prototype.request = function(config) {
    let promise = Promise.resolve(config)
    const chains = [dispatchRequest, undefined]

    //处理拦截器
    //请求拦截器的回调压入到chains的前面， request.handles =[]
    this.interceptors.request.handlers.forEach(item => {
        chains.unshift(item.fufilled, item.rejected)
    })

    //响应拦截器也处理一下
    this.interceptors.response.handlers.forEach(item => {
        chains.push(item.fufilled, item.rejected)
    })

    //遍历

    while (chains.length > 0) {
        promise = promise.then(chains.shift(), chains.shift())
    }
    return promise
}

function dispatchRequest(config) {
    return new Promise((res, rej) => {
        res({
            status: 200,
            statusText: 'OK'
        })
    })
}


//创建实例
let context = new Axios({})
//创建axios函数
let axios = Axios.prototype.request.bind(context)
//将context属性 config interceptors添加到axios属性 
Object.keys(context).forEach(key => {
    axios[key] = context[key]
})



//拦截器管理器构造函数
function InterceptorsManagers() {
    this.handlers = []
}

InterceptorsManagers.prototype.use = function(fufilled, rejected) {
    this.handlers.push({
        fufilled,
        rejected
    })
}

axios.interceptors.request.use(function(config) {
    console.log('1111')
    return config
}, function(error) {
    return Promise.reject(error)
})
axios.interceptors.request.use(function(config) {
    console.log('2222')
    return config
}, function(error) {
    return Promise.reject(error)
})
axios.interceptors.response.use(function(response) {
    console.log('3333')
    return response
}, function(error) {
    return Promise.reject(error)
})
axios.interceptors.response.use(function(response) {
    console.log('4444')
    return response
}, function(error) {
    return Promise.reject(error)
})

axios({
    method: 'get',
    url: 'http://localhost:3000/posts'
}).then(res => {
    console.log(res)
})
```

### 3.6 实现请求取消

```js
   //创建构造函数
    function Axios(config) {
        this.config = config
    }
    Axios.prototype.request = function(config) {
        return dispatchRequest(config)
    }

    function dispatchRequest(config) {
        return xhrAdapter(config)
    }


    function xhrAdapter(config) {
        return new Promise((resolve, reject) => {
            let xhr = new XMLHttpRequest()
            xhr.open(config.method, config.url)
            xhr.send()
            xhr.onreadystatechange = () => {
                    if (xhr.readyState == 4) {
                        if (xhr.status >= 200 && xhr.status < 300) {
                            resolve({
                                config: config,
                                data: xhr.response,
                                headers: xhr.getResponseHeader,
                                request: xhr,
                                status: xhr.statusText
                            })
                        } else {
                            reject('服务出错了!')
                        }
                    }
                }
                //关于取消请求的处理
            if (config.cancelToken) {
                //对cancelToken对象身上的promise对象指定成功的回调
                config.cancelToken.promise.then(value => {
                    xhr.abort()
                    reject(new Error('请求驳回'))
                })

            }
        })
    }

    const context = new Axios({})
    const axios = Axios.prototype.request.bind(context)

    function CancelToken(executor) {
        //声明一个变量
        var resolvePromise
        this.promise = new Promise(resolve => {
                resolvePromise = resolve
            })
            //调用executor函数
        executor(function() {
            resolvePromise()
        })
    }

    let cancel = null

    $('#send').click(() => {
        if (cancel != null) {
            cancel()
        }
        let cancelToken = new CancelToken(function(c) {
            cancel = c
        })
        axios({
            method: 'get',
            url: 'http://localhost:3000/posts/2',
            cancelToken: cancelToken
        }).then(response => {
            cancel = null
            console.log(response)
        })

    })

    $('#cancel').click(() => {
        cancel()
    })
```

### 3.7 全部代码整合

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="js/jquery-3.1.0.min.js"></script>

</head>

<body>
    <button id="send">发送请求</button>
    <button id="cancel">取消请求</button>
</body>

<script>
    function Axios(config) {
        this.config = config
        this.interceptors = {
            request: new InterceptorsManagers(),
            response: new InterceptorsManagers()
        }
    }

    //发送axios的所有请求必经之地
    Axios.prototype.request = function(config) {
        let promise = Promise.resolve(config)
            //将ajax中转器插入promise链中
        const chains = [dispatchRequest, undefined]
            //请求拦截器函数插入
        this.interceptors.request.hanlders.forEach(item => {
                chains.unshift(item.fufilled, item.rejected)
            })
            //响应拦截器函数插入
        this.interceptors.response.hanlders.forEach(item => {
            chains.push(item.fufilled, item.rejected)
        })

        //遍历 promise链
        while (chains.length > 0) {
            promise = promise.then(chains.shift(), chains.shift())
        }
        return promise
    }

    //给axios添加一些方法
    Axios.prototype.get = function(config) {
        return this.request({
            ...config,
            method: 'get'
        })
    }
    Axios.prototype.post = function(config) {
        return this.request({
            config,
            method: 'post'
        })
    }

    //ajax中转器 为了调用xhradpter
    function dispatchRequest(config) {
        return new xhrAdapter(config).then(response => {
            return response.data
        }, error => {
            throw error
        })
    }

    //拦截器的构造函数
    function InterceptorsManagers(config) {
        this.hanlders = []
    }
    //拦截器的添加方法 为了我们可以添加方法
    InterceptorsManagers.prototype.use = function(fufilled, rejected) {
            this.hanlders.push({
                fufilled,
                rejected
            })
        }
        //发送xhr
    function xhrAdapter(config) {
        return new Promise((resovle, reject) => {
            let xhr = new XMLHttpRequest()
            xhr.open(config.method, config.url)
            xhr.send()
            xhr.onreadystatechange = function() {
                if (xhr.readyState == 4) {
                    if (xhr.status >= 200 && xhr.status < 300) {
                        resovle({
                            config: config,
                            data: xhr.response,
                            headers: xhr.getResponseHeader,
                            request: xhr,
                            status: xhr.statusText
                        })
                    } else {
                        reject(new Error('请求失败'));
                    }
                }
            }
            if (config.cancelToken) {
                config.cancelToken.promise.then(res => {
                    xhr.abort()
                    reject(new Error('请求驳回'))
                })
            }
        })
    }
    //封装出一个当作对象使用的函数
    function createInstance(config) {
        let content = new Axios(config)
        let instance = Axios.prototype.request.bind(content)

        Object.keys(Axios.prototype).forEach(key => {
            instance[key] = Axios.prototype[key].bind(content)
        })
        Object.keys(content).forEach(key => {
            instance[key] = content[key]
        })
        return instance
    }


    function CancelToken(executor) {
        var resolvePromise
        this.promise = new Promise(resolve => {
            resolvePromise = resolve
        })
        executor(function() {
            resolvePromise()
        })
    }
    let axios = createInstance()

    //拦截器函数自定义添加
    axios.interceptors.request.use((config) => {
        console.log('请求拦截器1')
        return config
    }, (error) => {
        return Promise.reject(error)
    })
    axios.interceptors.request.use((config) => {
        console.log('请求拦截器2')
        return config
    }, (error) => {
        return Promise.reject(error)
    })
    axios.interceptors.response.use((response) => {
        console.log('响应拦截器1')
        return response
    }, (error) => {
        return Promise.reject(error)
    })
    axios.interceptors.response.use((response) => {
        console.log('响应拦截器2')
        return response
    }, (error) => {
        return Promise.reject(error)
    })





    // //作为函数使用
    // axios({
    //     method: 'get',
    //     url: 'http://localhost:3000/posts'
    // }).then(res => {
    //     console.log(res)
    // })

    // //作为对象使用
    // axios.get({
    //     url: 'http://localhost:3000/posts'
    // })]

    let cancel = null

    $('#send').click(() => {
        if (cancel != null) {
            cancel()
        }
        let cancelToken = new CancelToken(function(c) {
            cancel = c
        })
        axios({
            method: 'get',
            url: 'http://localhost:3000/posts/2',
            cancelToken: cancelToken
        }).then(response => {
            cancel = null
            console.log(response)
        })

    })

    $('#cancel').click(() => {
        cancel()
    })
</script>

</html>
```

