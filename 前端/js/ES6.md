# ES6

[TOC]



## 一、定义

ES6全称EcmaScript，是脚本语言的规范，而平时经常编写的JavaScript,是EcmaScript的一种实现，所以ES新特性其实指的就是JavaScript的新特性。



http://kangax.github.io/compat-table/es6/

![1645435466518](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645435466518.png)

## 二、ECMASript 6新特性

### 2.1 let 关键词

let变量声明的特点：

1. **变量不能重复声明**

2. **块级作用域**

   ```js
   {
       let girl = '123'
       }
   console.log(girl) //报错
   ```

3. **不存在变量提升**

   ```js
   console.log(song) //undefined
   var song = 345
   
   console.log(good) //报错
   let good = 123
   ```

4. **不影响作用域链**

   ```js
   {
       let school ='辛巴'
       function fn(){
           console.log(school)
       }
       fn()  //辛巴
   } 
   ```

#### 经典案例

```html
<div id="container">
    <div class="page-header">点击切换颜色</div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
</div>
<script>
    let items = document.getElementsByClassName('item')
    for (var i = 0; i < items.length; i++) {
        items[i].onclick = function() {
            items[i].style.background = 'pink'
        }
    }
    console.log(i) //3
</script>
```

![1645443067442](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645443067442.png)

这里使用var的话,i没有块级作用域，那么上升到全局的i就会变成3。肯定会报错。

所以使用let

```js
let items = document.getElementsByClassName('item')
for (let i = 0; i < items.length; i++) {
    items[i].onclick = function() {
        items[i].style.background = 'pink'
    }
}
console.log(i) //报错，块级作用域 ，所以全局找不到报错
```

### 2.2 const 关键词

const 关键字用来声明常量，const 声明有以下特点:

1. 一定要赋初始值

2. 标识符一般为大写

3. 不允许重复声明和修改

4. **块级作用域**

   ```js
   {
    const name = 12
   }
   console.log(name)//报错
   ```

5. **对于数组和对象的元素修改，不算做对常量的修改，不会报错！** 

   ```js
   const TEAM = ['uzi','mxlg','ming']
   TEAM.push('meiko')// ['uzi', 'mxlg', 'ming', 'meiko']
   TEAM=100//报错
   ```

应用场景：**声明对象类型使用 const，非对象类型声明选择let** 

### 2.3 变量的解构赋值

ES6允许按照一定模式从数组和对象中提取值，对变量进行赋值。

#### 数组的解构赋值

```js
const arr = ['刘强', '吴云', '俞文竹']
let [liu, wu, yu] = arr
```

#### 对象的解构赋值

```js
const liu={
    name:'刘强',
    age :24,
    fun:function(){
        console.log('我是刘强')
    }
}
let {name,age,fun} = liu
```

#### 复杂解构

```js
let wangfei = {
    name: 'wangfei',
    age: 18,
    songs: ['传奇', '六年', '暧昧'],
    history: [{
        name: '都为'
    }, {
        name: '李亚鹏'
    }]
}

let {
    songs: [one, two, three],
    history: [first, second]
} = wangfei
```

### 2.4 模板字符串

ES6引入新的声明字符串的方式，是增强版的字符串，用反引号（`）标识，特点：

1. **字符串中可以出现换行符**
2. **可以使用${xxx}形式输出变量**

```js
//定义字符串
let str = `<ul>
		<li>王菲</li>
		<li>李健</li>
		</ul>`
console.log(str) //'<ul>\n<li>王菲</li>\n<li>李健</li>\n</ul>'
// 变量拼接
let star ='杨浩'
let result = `${star}是个大叔阿瓜`
```

### 2.5 对象的简化写法

ES6允许在大括号里面，直接写入变量和函数，作为对象的属性和方法。

```js
let name = '刘强'
let slogn = '永远相信美好的时间即将发生'
let improve = function() {
    console.log('可以提高自己')
}

let liuqiang ={
    name,
    slogn,
    improve,
    change(){
        console.log('gaibian!')
    }
}
```

### 2.6 箭头函数

ES6 允许使用「箭头」（=>）定义函数。

```js
let fun = (arg1,agr2)=>{
    console.log(arg1,arg2)
}
```

注意点：

1. **this是静态的，this始终指向函数声明时所在作用域下的this的值**

   ```js
   function getName() {
       console.log(this.name)
   }
   
   let getName2 = () => {
       console.log(this.name)
   }
   
   //设置window的name属性
   window.name = '123'
   let liu = {
       name: 456
   }
   
   getName.apply(liu) //456
   getName2.apply(liu) //123
   ```

2. **不能作为构造函数实例化**

   ```js
   let Person = (name,age)=>{
       this.name = name
       this.age = age
   }
   let p = new Person('liuqiang',123)
   //报错 VM200:1 Uncaught TypeError: Person is not a constructor
   ```

3. **不能使用argument变量**

   ```js
   let fun = ()=>{
       console.log(arguments)
   }
   fun(1,2,3) //arguments is not defined
   ```

4. **箭头函数的简写**

   1)当形参有且只有一个时，可以简写

   ```js
   let add = n=>{
   console.log(n)
   }
   ```

   2)当代码体只有一条语句时，此时return必须省略，而且语句的执行结果就是函数的返回值

   ```js
   let pow = n => n*n
   console.log(pow(2))
   ```

#### 应用场景

1.点击div 两秒后这个div变色

```js
let container = document.getElementsByClassName('container')[0]
container.addEventListener('click', function() {
    setTimeout(() => {
        this.style.background = 'green'
    }, 2000)
})
```

2.从数组中返回偶数的元素

```js
const arr = [1, 6, 9, 10, 100, 25]
const result = arr.filter(item => item % 2 == 0)
```

结论：箭头函数适合与this无关的回调，定时器，数组的回调

箭头函数不适合与this有关的回调，事件回调，对象的方法

### 2.7 函数参数默认值

ES6允许给函数参数赋值初始值，一般具有默认值的形参参数，默认靠后。

```js
function add(a, b, c = 100) {
    return a + b + c
}
let result = add(1, 2)
console.log(result)
```

与解构赋值结合

```js
function connect({ host, username, password, port }) {
    console.log(host)
    console.log(username)
    console.log(password)
    console.log(port)
}

connect({
    host: 'localhost',
    username: 'root',
    password: 'root',
    port: 'root'
})
```

### 2.8 rest函数参数

ES5获取实参的方式

```js
function date() {
    console.log(arguments)
}

date(1, 2, 34)
```

ES6引入rest参数，用于获取函数的参数，用来代替arguments。

```js
function date1(a, b, ...args) {
    console.log(args)
}

date1(1, 2, 4, 3, 34)//[4, 3, 34]
```

**rest参数必须是最后一个参数，非常适合不定个数参数函数的场景**

### 2.9 spread扩展运算符

[...]扩展运算符能将数组转换为逗号分隔的参数序列

1. 展开数组

    ```js
    const names = ['刘强', '俞文竹', '吴云']
    console.log(...names) //刘强 俞文竹 吴云
    ```
    
2. 展开对象

    ```js
    let skillone = {
        q: '致命打击'
    }
    let skilltwo = {
        w: 'yongqi'
    }
    let skillThree = {
        e: '审判'
    };
    let skillFour = {
        r: '德玛西亚正义'
    };
    
    let gailun = {...skillone, ...skilltwo, ...skillThree, ...skillFour }
    //{q: '致命打击', w: 'yongqi', e: '审判', r: '德玛西亚正义'}
    ```

### 2.10 Symbol基本使用

ES6引入了新的原始数据类型，表示独一无二的值。

它是 JavaScript 语言的第七种数据类型，是一种类似于字符串的数据类型。

1. Symbol的值是唯一的，用来解决命名冲突的问题
2. Symbol值不能与其他数据进行运算
3. Symbol定义的对象属性**不能使用for...in循环**遍历，但是**可以使用Reflect.ownKeys来获取对象的所有键名**

```js
//创建Symbol
let s = Symbol()
console.log(s, typeof s)  //Symbol()  'symbol'

//添加标识的symbol
let s2 = Symbol('刘强')
let s3 = Symbol('刘强')
console.log(s2===s3) //false

//使用 Symbol for 定义
//ymbol for 被登记在全局环境中供搜索
let s4 = Symbol.for('刘强')
let s5 = Symbol.for('刘强')
console.log(s4===s5) //true
```

![1645505490923](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645505490923.png)

#### 对象中添加Symbol类型的属性

```js
//向对象中添加方法 up down
let method = {
    up: Symbol(),
    down: Symbol()
}

game[method.up] = function() {
    console.log('up')
}
game[method.down] = function() {
    console.log('down')
}

console.log(game) //{Symbol(): ƒ, Symbol(): ƒ}

let youxi = {
    name: '狼人杀',
    [Symbol('say')]: function() {
        console.log('说话')
    },
    [Symbol('zibao')]: function() {
        console.log('zibao')
    }
}

```

#### Symbol内置属性

Symbol.hasInstance 

当其他对象使用 instanceof 运算符，判断是否为该对象的实例时，会调用这个方法 

```js
class Person {
    static[Symbol.hasInstance](parm) {
        console.log(parm)
        console.log('检测类型')
    }
}

let o = { name: 123 }
console.log(o instanceof Person)
//{name: 123} 检测类型 false
```

![1645513094736](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645513094736.png)

### 2.11迭代器

迭代器是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署Iterator接口，就可以完成遍历操作。

1. ES6创造了一种新的遍历命令for...of循环，Iterator接口主要供for...of消费
2. 原生具备iterator接口的数据
   - Array
   - Arguments
   - Set
   - Map
   - String
   - TypedArray
   - NodeList
3. 工作原理
   1. 创建一个指针对象，指向当前数据结构的起始位置
   2. 第一次调用对象的next方法，指针自动指向数据结构的第一个成员
   3. 接下来不断调用next方法，指针一直往后移动，直到指向最后一个成员
   4. 每调用next方法返回一个包含value和done属性的对象

```js
const fruit = ['西瓜', '草莓', '哈密瓜', '车厘子']

for (let v in fruit) {
    console.log(v)
}
//0
//1
//2
//3
for (let v of fruit) {
    console.log(v)
}
// 西瓜
// 草莓
// 哈密瓜
// 车厘子
```

```js
const fruit = ['西瓜', '草莓', '哈密瓜', '车厘子']

let iterator = fruit[Symbol.iterator]()

console.log(iterator.next()) //{value: '西瓜', done: false}
console.log(iterator.next()) //{value: '草莓', done: false}
console.log(iterator.next()) //{value: '哈密瓜', done: false}
console.log(iterator.next()) //{value: '车厘子', done: false}
console.log(iterator.next()) //{value: undefined, done: true}
```

#### 自定义遍历数据

```js
const banji = {
    name: '终极一班',
    students: ['刘强', '吴云', '若家']
}

for (let v of banji) {
    console.log(v)
} //Uncaught TypeError: banji is not iterable

for (let v of banji.students) {
    console.log(v)
}
//刘强
//吴云
//若家
```

自定义迭代器

```js
const banji = {
    name: '终极一班',
    students: ['刘强', '吴云', '若家'],
    [Symbol.iterator]() {
        let index = 0;
        return {
            next: () => {
                if (index < this.students.length) {
                    const result = { value: this.students[index], done: false }
                    index++
                    return result
                } else {
                    return { value: undefined, done: true }
                }
            }
        }
    }
}

for (let v of banji) {
    console.log(v)
} 
//刘强
//吴云
//若家
```

### 2.12 生成器

生成器其实就是一个特殊的函数，一种异步编程解决方案。

yield相当于分隔符，将函数分割成几部分

```js

function* gen() {

    console.log('第一部分')

    yield 'yeild1'

    console.log('第二部分')

    yield 'yeild2'

    console.log('第三部分')

    yield 'yeild3'

    console.log('第四部分')
}

let iterable = gen()
iterable.next() //第一部分
//{value: 'yeild1', done: false}
iterable.next()
//第二部分
//{value: 'yeild2', done: false}
iterable.next()
//第三部分
//{value: 'yeild3', done: false}
iterable.next()
//第四部分
//{value: undefined, done: true}


//遍历 每次返回的是yield后面的字面量

for (let v of gen()) {
    console.log(v)
}

执行第1部分  打印yield1
执行第2部分  打印yield2
执行第3部分  打印yield2
执行第4部分  遍历结束 打印undefined
```

代码说明

1. *的位置没有限制

2. 生成器函数返回的结果是迭代器对象，调用**迭代器对象的next方法可以得到yield语句后的值**

   ```js
   let iterable = gen()
   console.log(iterable.next()) //{value: 'yeild1', done: false}
   ```

3. **yeild相当于函数的暂停标记，也可以认为是函数的分割符，**每调用一次next，执行一段代码

   ```js
   let iterable = gen()
   iterable.next() //第一部分
   //{value: 'yeild1', done: false}
   iterable.next()
   //第二部分
   //{value: 'yeild2', done: false}
   iterable.next()
   //第三部分
   //{value: 'yeild3', done: false}
   iterable.next()
   //第四部分
   //{value: undefined, done: true}
   ```

4. **next方法可以传递实参，作为yield语句的返回值**

   ```js
   function* fun(arg) {
       console.log(arg)
       let y1 = yield '第1段'
       console.log(y1)
       let y2 = yield '第2段'
       console.log(y2)
       let y3 = yield '第3段'
       console.log(y3)
   }
   
   let it = fun('初始参数')
   console.log(it.next())
   console.log(it.next('第1段的返回值'))
   console.log(it.next('第2段的返回值'))
   console.log(it.next('第3段的返回值'))
   ```

![1645535301432](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645535301432.png)

#### 生成器函数实例

1s后在控制台输出111 

2s后再控制台输出222

3s后再控制台输出222

```js
function* prints() {

    yield one()
    yield two()
    yield three()
}
let it = prints()

function one() {
    setTimeout(() => {
        console.log(111)
        it.next()
    }, 1000);
}

function two() {
    setTimeout(() => {
        console.log(222)
        it.next()
    }, 2000);
}

function three() {
    setTimeout(() => {
        console.log(333)
    }, 3000);
}

it.next()
```

获取用户数据，订单数据，商品数据

```js
function* result() {
    let one = yield getUsers()
    console.log(one, '在')
    let two = yield getOrders()
    console.log(two, '中买了')
    let three = yield getGoods()
    console.log(three)
}
let it = result()


function getUsers() {
    setTimeout(() => {
        let username = '刘强'
        it.next(username)
    }, 1000);
}

function getOrders() {
    setTimeout(() => {
        let Orders = '订单1'
        it.next(Orders)
    }, 1000);
}

function getGoods() {
    setTimeout(() => {
        let Goods = '沙琪玛'
        it.next(Goods)
    }, 1000);
}


it.next('刘强')
```

### 2.13 Promise

Promise是ES6引入的异步编程的新解决方案。语法上Promise是一个构造函数，用来封装异步操作并可以获取成功或失败的结果。

1. Promise 构造函数:promise(exctor){}
2. Promise.prototype.then方法
3. Promise.prototype.catch方法

```js
//实例化 promise对象
const p = new Promise(function(resolve, reject) {
    setTimeout(function() {
        let data = '数据库中数据'
        resolve(data)
    }, 1000)
    
    // setTimeout(function() {
    //     let err = '报错了'
    //     reject(err)
    // }, 2000)

})

p.then(function(resolve) {
    console.log('成功信息：', resolve)
}, function(reject) {
    console.error('错误信息：', reject)
})
```

resolve和reject只会调用一次，只有一种状态。

#### Promise对象

##### Promise的状态

实例对象中的一个属性 【PromiseState】

- **pending	未决定的**
- **resoved/fullfilled	成功**
- **rejected	失败**

1. pending变成resolved
2. pending变成rejected

说明：只有这两种，且一个prmoise对象只能改变一次。无论变为成功还是失败，都会有一个结果数据。成果的结果数据一般未value,失败的结果数据一般为reason

------

##### Promise对象的值

实例对象的另一属性 【PromiseResult】

保存着对象异步任务【成功/失败的结果】

- resolve
- reject

#### promise读取文件

**普通读取文件**

```js
//引入fs模块
const fs = require('fs')

//调用方法读取文件
fs.readFile('./论语.txt', (err, data) => {
    //如果失败 ，抛出错误
    if (err) throw err
    //如果成功 ，输出内容
    console.log(data.toString())
})
```

**promise读取文件**

```js
//引入fs模块
const fs = require('fs')

const p = new Promise((resolve, reject) => {
    fs.readFile('./论语.txt', (err, data) => {
        if (err) reject(err)
        resolve(data)
    })
})

p.then((resolve) => {
    console.log(resolve.toString())
}, (reject) => {
    console.log(reject)
})
```

**promise封装fs读取文件操作**

```js
//封装一个函数mineReadFile 读取文件内容

function mineReadFile(path) {
    return new Promise((res, rej) => {
        require('fs').readFile(path, (err, data) => {
            if (err) {
                rej(err)
            } else {
                res(data)
            }
        })
    })
}

mineReadFile('1.txt').then(res => {
    console.log(res.toString())
}, rej => {
    console.log(rej)
})
```

#### util.promisify进行promise转化

传入一个**错误优先回调的函数**（err,data）=>作为参数，比如简单文件传入这样的函数，就可以返回一个promise版本的函数。

```js
const util = require('util')
const fs = require('fs')

//返回一个新的函数
let minReadFile = util.promisify(fs.readFile)

minReadFile('1.txt').then(value => {
    console.log(value.toString   ())
})
```

#### promise封装ajax

```js
const p = new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest()
    xhr.open('get', 'http://localhost:8001/ajax_promise')
    xhr.send()
    xhr.onreadystatechange = () => {
        if (xhr.readyState == 4) {
            if (xhr.status >= 200 && xhr.status < 300) {
                resolve(xhr.response)
            } else {
                reject(xhr.statusText)
            }
        }
    }
})
//回调函数写这里
p.then(resolve => {
    console.log(resolve)
}, reject => {
    console.error(reject)
})
```

#### Promise的API

##### Promise构造函数：Promise(excutor){}

![1645945285134](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645945285134.png)

注意：**exector会在Promise内部立即调用，异步操作在执行其中执行。**

```js
let p = new Promise((resolve, reject) => {
    console.log(111)
})

console.log(222)

//111
//222
```

##### Promise.prototype.then方法：(onResolved,onRejected)=>{}

![1645945462929](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645945462929.png)

调用then方法，then返回的结果是**Promise对象**，对象状态由回调函数的执行结果决定

**如果回调函数中返回的结果是非Promise类型的属性，状态为成功，返回值为对象的成功的值。**

```js

const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('第一个promise')
    }, 1000)
})

let p2 = p1.then(res => {
    console.log(res)
    //返回非promise
    //return '第一个promise'
    //返回promise
    return new Promise((res, rej) => {
        res('返回第二个promise')
    })
})

console.log(p2)
```

![1645604361229](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645604361229.png)

**如果回调函数中返回的结果是Promise类型的属性，返回的值就是resolve或者reject的值**

##### 多个文件内容读取

```js
const p1 = new Promise((res, rej) => {
    fs.readFile('./1.txt', (err, data) => {
        if (err) rej(err)
        res(data.toString())
    })
})
p1.then(res => {
    return new Promise((res1, rej) => {
        fs.readFile('./2.txt', (err, data) => {
            if (err) rej(err)
            res1(res + data.toString())
        })
    })
})
    .then(res => {
    return new Promise((res2, rej) => {
        fs.readFile('./3.txt', (err, data) => {
            if (err) rej(err)
            res2(res + data.toString())
        })
    })
}).then(res => {
    console.log(res)
})
```

##### Promise.prototype.catch方法：(onRejected)=>{}

![1645945510845](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645945510845.png)

只有失败的回调

![1645606455263](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645606455263.png)

#### Promise的方法

以下是Promise函数的方法，不是实例对象的方法

##### Promise.resolve方法：(value)=>{}

![1645945672926](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645945672926.png)

**参数的参数有非promise和promise的，反正返回都是promise对象！！！**

```js
//如果参数的参数是非promise类型的对象，则返回的结果为成功的Promise对象。
let p1 = Promise.resolve(521);
console.log(p1) //Promise { 521 }

//如果传入的参数为Promise对象，则参数的结果决定了resovle的结果
let p2 = Promise.resolve(new Promise((resolve, reject) => {
    resolve('ok')
}))
console.log(p2) //Promise { 'ok' }
```

##### Promise.reject方法：(reason)=>{}

同理和实例对象的catch方法类似

![1645946104845](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645946104845.png)

```js
//如果参数的参数是非promise类型的对象，则返回的结果为失败的Promise对象。
let p3 = Promise.reject(521);
console.log(p3) //Promise {<rejected>: 521}

let p4 = Promise.reject(new Promise((resolve, reject) => {
    reject('fail')
}))
p4.catch(rej => { //如果参数的参数是非promise类型的对象，则返回的结果为失败的Promise对象。
    let p3 = Promise.reject(521);
    console.log(p3) //Promise {<rejected>: 521}
    console.log(rej)
})
```

##### Promise.all方法：(promises)=>{}

![1645946685325](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645946685325.png)

如果都成功了，返回的结果值是三个成果的数组

```js
let p1 = new Promise((res, rej) => {
    res('p1')
})

let p2 = Promise.resolve('p2')
let p3 = Promise.resolve('p3')

const result = Promise.all([p1, p2, p3])
console.log(result)
```

![1645946880392](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645946880392.png)

如果有一个失败了,返回的结果值是**最先失败的promise的结果**

```js
let p1 = new Promise((res, rej) => {
    res('p1')
})

let p2 = Promise.reject('p2')
let p3 = Promise.reject('p3')

const result = Promise.all([p1, p2, p3])
console.log(result)
```

![1645946975013](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645946975013.png)

##### Promise.race方法：(promises)=>{}

![1645951290416](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645951290416.png)

```js
let p1 = new Promise((res, rej) => {
    setTimeout(() => {
        res('p1')
    }, 1000)
})

let p2 = Promise.resolve('p2')
let p3 = Promise.resolve('p3')

const result = Promise.race([p1, p2, p3])
console.log(result) 

//因为p2最先完成，所以返回p2
//Promise {<pending>}
//[[Prototype]]: Promise
//[[PromiseState]]: "fulfilled"
//[[PromiseResult]]: "p2"
```

#### Promise的关键问题

**1.如何改变promise的状态**

![1645951666301](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645951666301.png)

![1645951829677](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645951829677.png)

**2.promise指定多个成功/失败回调函数，都会调用么？**

当状态改变之后，都会调用。如果状态没有改变，一直是pending时，则都不会调用。

```js
let p1 = new Promise((res, rej) => {
    res('p1')
})


p1.then(value => {
    console.log(111)
})

p1.then(value => {
    console.log(222)
})

//111
//222
```

**3.※改变promise状态和指定回调函数先后？※**

1. 都有可能，正常情况下是先指定回调再改变状态，但是也可以改状态再指定回调
2. 如何先改状态再指定回调？
   - 在执行器中直接调用resovle/reject，即同步任务
   - 延长时间调用then
3. 什么时候才能得到数据(即什么时候回调执行 )
   - 如果先指定的回调，那么当状态发生改变时，回调函数就会调用，得到数据
   - 如果先改变的状态，那当指定回调时，会调函数就会调用，得到数据

**4.Promise.then()返回值返回新的promise的结果状态由什么决定？**

![1645952795518](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645952795518.png)

**5.Promise如何串联多个操作任务？**

1. Promise的then()返回一个新的Promise,可以看成then()的链式调用

2. 通过then的链式调用串联多个同步/异步任务

   ```js
   let p = new Promise((res, rej) => {
       setTimeout(() => {
           res('111')
       }, 1000)
   })
   
   p.then(value => {
       console.log(value) //111
       return new Promise((res, rej) => {
           res('222')
       })
   }).then(value => {
       console.log(value)///222
       return '我爱你' 
   }).then(value => {
       console.log(value) //我爱你
   }).then(value => {
       console.log(value) //undefined
   })
   ```

**6.Promise异常穿透**

1. 当使用promise的then链式调用时，可以在最后指定失败的回调

2. 前面任何操作除了异常，都会传到最后失败的回调中处理。

   ```js
   let p1 = new Promise((res, rej) => {
       setTimeout(() => {
           rej('我爆了')
       }, 1000)
   })
   
   p1.then(value => {
       return new Promise((res, rej) => {
           res('222')
       })
   }).then(value => {
       console.log(value)
   }).then(value => {
       console.log(value)
   }).catch(rej => {
       console.log(rej)
   })
   ```

   这里有错 直接就可以跳到最后。

**7.中断promise链**

当使用promise的 then链式调用时，在中间中断，不再调用后面的回调函数。

方法:**在回调函数中返回一个pending状态的promise对象**

```js
let p2 = new Promise((res, rej) => {
    setTimeout(() => {
        res('我爆了')
    }, 1000)
})

p2.then(value => {
    console.log(111)
        //有且只有一种方式
    return new Promise(() => {}) //状态不改变 下面都不执行了
}).then(value => {
    console.log(222)
}).then(value => {
    console.log(333)
})
```

#### 手写Promise!!!

##### 基本功能

调用promise

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="promise.js"></script>
    <script>
        let p = new Promise((res, rej) => {
            res('OK')
            throw '123'
        })

        console.log(p)
        p.then(res => {
            console.log(res)
        }, rej => {
            console.log(rej)
        })
    </script>

    <body>

    </body>

</html>
```

promise代码

```js
//声明构造函数
function Promise(executor) {

    //添加属性
    this.PromiseState = 'pending'
    this.PromiseResult = null
    const self = this

    function resolve(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'fulfilled'
            //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data

    }

    function reject(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'rejected'
            //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data
    }
    //同步调用[执行器函数]
    try {
        executor(resolve, reject)
    } catch (e) {
        reject(e)
    }

}

//添加then方法
Promise.prototype.then = function(onResolved, onRejected) {
    if (this.PromiseState == 'fulfilled') {
        onResolved(this.PromiseResult)
    } else if (this.PromiseState == 'rejected') {
        onRejected(this.PromiseResult)
    }


}
```

##### 异步任务回调的执行

上述代码中 一旦由异步任务，就不管用了。需要加上pending的状态！

```js
let p = new Promise((res, rej) => {
    setTimeout(() => {
        res('OK')
    }, 1000)

})

console.log(p)
p.then(res => {
    console.log(res)
}, rej => {
    console.log(rej)
})

```

promise代码

```js
//声明构造函数
function Promise(executor) {

    //添加属性
    this.PromiseState = 'pending'
    this.PromiseResult = null
    const self = this
    this.callback = {}

    function resolve(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'fulfilled'
            //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data

        if (self.callback.onResolved) {
            self.callback.onResolved(data)
        }
    }

    function reject(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'rejected'
            //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data

        if (self.callback.onRejected) {
            self.callback.onRejected(data)
        }
    }
    //同步调用[执行器函数]
    try {
        executor(resolve, reject)
    } catch (e) {
        reject(e)
    }

}

//添加then方法
Promise.prototype.then = function(onResolved, onRejected) {
    if (this.PromiseState == 'fulfilled') {
        onResolved(this.PromiseResult)
    } else if (this.PromiseState == 'rejected') {
        onRejected(this.PromiseResult)
    }

    if (this.PromiseState == 'pending') {
        //保存回调函数
        this.callback = {
            onResolved: onResolved,
            onRejected: onRejected
        }
    }

}
```

##### 指定多个回调

```js
let p = new Promise((res, rej) => {
    setTimeout(() => {
        res('OK')
        // throw '123'
    }, 1000)

})


p.then(res => {
    console.log(res)
}, rej => {
    console.log(rej)
})
p.then(res => {
    alert(res)
}, rej => {
    console.log(rej)
})

console.log(p)
```

promise代码

```js
//声明构造函数
function Promise(executor) {

    //添加属性
    this.PromiseState = 'pending'
    this.PromiseResult = null
    const self = this
    this.callbacks = []

    function resolve(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'fulfilled'
        //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data

        self.callbacks.forEach(item => {
            item.onResolved(data)
        })
    }

    function reject(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'rejected'
        //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data

        self.callbacks.forEach(item => {
            item.onRejected(data)
        })
    }
    //同步调用[执行器函数]
    try {
        executor(resolve, reject)
    } catch (e) {
        reject(e)
    }

}

//添加then方法
Promise.prototype.then = function(onResolved, onRejected) {
    if (this.PromiseState == 'fulfilled') {
        onResolved(this.PromiseResult)
    } else if (this.PromiseState == 'rejected') {
        onRejected(this.PromiseResult)
    }

    if (this.PromiseState == 'pending') {
        //保存回调函数
        this.callbacks.push({
            onResolved: onResolved,
            onRejected: onRejected
        })
    }

}
```

##### 同步修改状态then方法结果返回

```js
let p = new Promise((res, rej) => {
    // setTimeout(() => {
    //     res('OK')
    //         // throw '123'
    // }, 1000)
    res('OK')
})


const err = p.then(res => {
    console.log(res)
    return new Promise((res1, rej1) => {
        res1('12332')
    })
})

console.log(err)
```



```js
//声明构造函数
function Promise(executor) {

    //添加属性
    this.PromiseState = 'pending'
    this.PromiseResult = null
    const self = this
    this.callbacks = []

    function resolve(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'fulfilled'
            //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data

        self.callbacks.forEach(item => {
            item.onResolved(data)
        })
    }

    function reject(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'rejected'
            //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data

        self.callbacks.forEach(item => {
            item.onRejected(data)
        })
    }
    //同步调用[执行器函数]
    try {
        executor(resolve, reject)
    } catch (e) {
        reject(e)
    }

}

//添加then方法
Promise.prototype.then = function(onResolved, onRejected) {
    return new Promise((res, rej) => {
        if (this.PromiseState == 'fulfilled') {
            try {
                //获取回调函数的执行结果
                let result = onResolved(this.PromiseResult)
                    //判断结果是否为promise
                if (result instanceof Promise) {
                    result.then(v => {
                        res(v)
                    }, r => {
                        rej(r)
                    })
                } else {
                    res(result)
                }
            } catch (e) {
                onRejected(e)
            }

        } else if (this.PromiseState == 'rejected') {
            onRejected(this.PromiseResult)
        }

        if (this.PromiseState == 'pending') {
            //保存回调函数
            this.callbacks.push({
                onResolved: onResolved,
                onRejected: onRejected
            })
        }
    })
}
```

##### 异步修改状态then方法结果返回

```js
let p = new Promise((res, rej) => {
    setTimeout(() => {
        res('OK')
        // throw '123'
    }, 1000)
})


const err = p.then(res => {
    console.log(res)
    return '1232'
}, rej => {
    console.log(rej)
})

console.log(err)
</script>
```

```js
//声明构造函数
function Promise(executor) {

    //添加属性
    this.PromiseState = 'pending'
    this.PromiseResult = null
    const self = this
    this.callbacks = []

    function resolve(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'fulfilled'
            //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data

        self.callbacks.forEach(item => {
            item.onResolved(data)
        })
    }

    function reject(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'rejected'
            //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data

        self.callbacks.forEach(item => {
            item.onRejected(data)
        })
    }
    //同步调用[执行器函数]
    try {
        executor(resolve, reject)
    } catch (e) {
        reject(e)
    }

}

//添加then方法
Promise.prototype.then = function(onResolved, onRejected) {
    const self = this
    return new Promise((res, rej) => {
        if (this.PromiseState == 'fulfilled') {
            try {
                //获取回调函数的执行结果
                let result = onResolved(this.PromiseResult)
                    //判断结果是否为promise
                if (result instanceof Promise) {
                    result.then(v => {
                        res(v)
                    }, r => {
                        rej(r)
                    })
                } else {
                    res(result)
                }
            } catch (e) {
                onRejected(e)
            }

        } else if (this.PromiseState == 'rejected') {
            onRejected(this.PromiseResult)
        }
        //判断pending状态
        if (this.PromiseState == 'pending') {
            //保存回调函数
            this.callbacks.push({
                onResolved: function() {
                    try {
                        let result = onResolved(self.PromiseResult)
                        if (result instanceof Promise) {
                            result.then(v => {
                                res(v)
                            }, r => {
                                rej(r)
                            })
                        } else {
                            res(result)
                        }
                    } catch (e) {
                        rej(e)
                    }

                },
                onRejected: function() {
                    try {
                        let result = onRejected(self.PromiseResult)
                        if (result instanceof Promise) {
                            result.then(v => {
                                res(v)
                            }, r => {
                                rej(r)
                            })
                        } else {
                            res(result)
                        }
                    } catch (e) {
                        res(e)
                    }

                }
            })

        }
    })
}
```

##### 补全then并封装函数

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="promise.js"></script>
    <script>
        let p = new Promise((res, rej) => {
            setTimeout(() => {
                    res('OK')
                        // throw '123'
                }, 1000)
                //rej('fail')
        })


        const err = p.then(res => {
            console.log(res)
            return '1232'
        }, rej => {
            console.log(rej)
                // return 'sss'
        })

        console.log(err)
    </script>

    <body>

    </body>

</html>
```

```js
//声明构造函数
function Promise(executor) {

    //添加属性
    this.PromiseState = 'pending'
    this.PromiseResult = null
    const self = this
    this.callbacks = []

    function resolve(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'fulfilled'
            //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data

        self.callbacks.forEach(item => {
            item.onResolved(data)
        })
    }

    function reject(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'rejected'
            //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data

        self.callbacks.forEach(item => {
            item.onRejected(data)
        })
    }
    //同步调用[执行器函数]
    try {
        executor(resolve, reject)
    } catch (e) {
        reject(e)
    }

}

//添加then方法
Promise.prototype.then = function(onResolved, onRejected) {
    const self = this
    return new Promise((res, rej) => {
        //封装函数
        function callback(type) {
            try {
                let result = type(self.PromiseResult)
                if (result instanceof Promise) {
                    result.then(v => {
                        res(v)
                    }, r => {
                        rej(r)
                    })
                } else {
                    res(result)
                }

            } catch (e) {
                rej(e)
            }

        }
        if (this.PromiseState == 'fulfilled') {
            callback(onResolved)

        } else if (this.PromiseState == 'rejected') {
            callback(onRejected)
        }
        //判断pending状态
        if (this.PromiseState == 'pending') {
            //保存回调函数
            this.callbacks.push({
                onResolved: function() {
                    callback(onResolved)
                },
                onRejected: function() {
                    callback(onRejected)
                }
            })

        }
    })
}
```

##### 添加catch方法

```js
//添加catch方法
Promise.prototype.catch = function(onRejected) {
    return this.then(undefined, onRejected)
}
```

##### resovle方法封装

```js
Promise.resolve = (value) => {
    return new Promise((res, rej) => {
        if (value instanceof Promise) {
            value.then(v => {
                res(v)
            }, r => {
                rej(r)
            })
        } else {
            res(value)
        }

    })
}
```

##### rejected方法封装

```js
Promise.reject = (rej) => {
    return new Promise((resovle, reject) => {
        reject(rej)
    })
}
```

##### all封装

```js
let r1 = Promise.resolve('resolve1')
let r2 = Promise.reject('resolve2')
let r3 = Promise.reject('resolve3')
let result = Promise.all([r1, r2, r3])
console.log(result)
```

```js
Promise.all = (Promises) => {
    //返回结果是promise的对象
    return new Promise((resovle, reject) => {
        let count = 0
        let arr = []
        //遍历
        for (let i = 0; i < Promises.length; i++) {
            Promises[i].then(v => {
                count++
                arr[i] = v
                if (count == Promises.length) {
                    resovle(arr)
                }
            }, r => {
                reject(r)
            })
        }
    })
}
```

##### race封装

```js
let ra1 = Promise.resolve('resolve1')
let ra2 = Promise.resolve('resolve2')
let ra3 = Promise.resolve('resolve3')
let resulta = Promise.race([ra1, ra2, ra3])
console.log(resulta)
```

```js

Promise.race = (Promises) => {
    //返回结果是promise的对象
    return new Promise((resovle, reject) => {
        //遍历
        for (let i = 0; i < Promises.length; i++) {
            Promises[i].then(v => {
                resovle(v)
            }, r => {
                reject(r)
            })
        }
    })
}
```

##### then方法回调的异步执行

```js

        let p1 = new Promise((res, rej) => {
            res(111)
            console.log('111')
        })
        p1.then(value => {
            console.log(222)
        })

        console.log(333)
、、一般情况下要实现 1 3 2
```

所以要添加定时器

```js
//声明构造函数
function Promise(executor) {

    //添加属性
    this.PromiseState = 'pending'
    this.PromiseResult = null
    const self = this
    this.callbacks = []

    function resolve(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'fulfilled'
            //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data
        ！！！！这里！！！！
        setTimeout(() => {
            self.callbacks.forEach(item => {
                item.onResolved(data) 
            })
        })
    }

    function reject(data) {
        //判断状态，只能运行一次
        if (self.PromiseState != 'pending') {
            return
        }
        //1.修改对象的状态 (PromiseState)
        self.PromiseState = 'rejected'
            //2.设置对象结果值 (PromiseResult)
        self.PromiseResult = data
        ！！！！这里！！！！
        setTimeout(() => {
            self.callbacks.forEach(item => {
                item.onRejected(data)
            })
        })

    }
    //同步调用[执行器函数]
    try {
        executor(resolve, reject)
    } catch (e) {
        reject(e)
    }

}

//添加then方法
Promise.prototype.then = function(onResolved, onRejected) {
    const self = this
        //如果失败回调函数为空
    if (typeof onRejected != 'function') {
        onRejected = rej => {
            throw rej
        }
    }
    if (typeof onResolved != 'function') {
        onResolved = res => res

    }
    return new Promise((res, rej) => {
        //封装函数
        function callback(type) {
            try {
                let result = type(self.PromiseResult)
                if (result instanceof Promise) {
                    result.then(v => {
                        res(v)
                    }, r => {
                        rej(r)
                    })
                } else {
                    res(result)
                }

            } catch (e) {
                rej(e)
            }

        }
        if (this.PromiseState == 'fulfilled') {
            ！！！！这里！！！！
            setTimeout(() => {
                callback(onResolved)
            })


        } else if (this.PromiseState == 'rejected') {
            ！！！！这里！！！！
            setTimeout(() => {
                callback(onRejected)
            })

        }
        //判断pending状态
        if (this.PromiseState == 'pending') {
            //保存回调函数
            this.callbacks.push({
                onResolved: function() {
                    callback(onResolved)
                },
                onRejected: function() {
                    callback(onRejected)
                }
            })

        }
    })
}

```

##### class版本的实现！！

```JS
class Promise {
    constructor(executor) {
        //添加属性
        this.PromiseState = 'pending'
        this.PromiseResult = null
        const self = this
        this.callbacks = []

        function resolve(data) {
            //判断状态，只能运行一次
            if (self.PromiseState != 'pending') {
                return
            }
            //1.修改对象的状态 (PromiseState)
            self.PromiseState = 'fulfilled'
            //2.设置对象结果值 (PromiseResult)
            self.PromiseResult = data
            setTimeout(() => {
                self.callbacks.forEach(item => {
                    item.onResolved(data)
                })
            })
        }
        function reject(data) {
            //判断状态，只能运行一次
            if (self.PromiseState != 'pending') {
                return
            }
            //1.修改对象的状态 (PromiseState)
            self.PromiseState = 'rejected'
            //2.设置对象结果值 (PromiseResult)
            self.PromiseResult = data
            setTimeout(() => {
                self.callbacks.forEach(item => {
                    item.onRejected(data)
                })
            })
        }
        //同步调用[执行器函数]
        try {
            executor(resolve, reject)
        } catch (e) {
            reject(e)
        }
    }

    //添加then方法
    then(onResolved, onRejected) {
        const self = this
        //如果失败回调函数为空
        if (typeof onRejected != 'function') {
            onRejected = rej => {
                throw rej
            }
        }
        if (typeof onResolved != 'function') {
            onResolved = res => res

        }
        return new Promise((res, rej) => {
            //封装函数
            function callback(type) {
                try {
                    let result = type(self.PromiseResult)
                    if (result instanceof Promise) {
                        result.then(v => {
                            res(v)
                        }, r => {
                            rej(r)
                        })
                    } else {
                        res(result)
                    }

                } catch (e) {
                    rej(e)
                }

            }
            if (this.PromiseState == 'fulfilled') {
                setTimeout(() => {
                    callback(onResolved)
                })


            } else if (this.PromiseState == 'rejected') {
                setTimeout(() => {
                    callback(onRejected)
                })

            }
            //判断pending状态
            if (this.PromiseState == 'pending') {
                //保存回调函数
                this.callbacks.push({
                    onResolved: function() {
                        callback(onResolved)
                    },
                    onRejected: function() {
                        callback(onRejected)
                    }
                })

            }
        })
    }

    catch (onRejected) {
        return this.then(undefined, onRejected)
    }

    //静态成员 属于类不属于实例对象
    static resolve(value) {
        return new Promise((res, rej) => {
            if (value instanceof Promise) {
                value.then(v => {
                    res(v)
                }, r => {
                    rej(r)
                })
            } else {
                res(value)
            }

        })
    }
    static reject(rej) {
        return new Promise((resovle, reject) => {
            reject(rej)
        })
    }

    static all(Promises) {
        //返回结果是promise的对象
        return new Promise((resovle, reject) => {
            let count = 0
            let arr = []
            //遍历
            for (let i = 0; i < Promises.length; i++) {
                Promises[i].then(v => {
                    count++
                    arr[i] = v
                    if (count == Promises.length) {
                        resovle(arr)
                    }
                }, r => {
                    reject(r)
                })
            }
        })
    }

    static race(Promises) {
        //返回结果是promise的对象
        return new Promise((resovle, reject) => {
            //遍历
            for (let i = 0; i < Promises.length; i++) {
                Promises[i].then(v => {
                    resovle(v)
                }, r => {
                    reject(r)
                })
            }
        })
    }
}
```

#### async与await

##### async

1. 函数的返回值是promise对象
2. promise对象结果由async函数执行的返回值决定

```js
    async function main() {
        return '这是async'
    }
    async function main1() {
        return new Promise((res, rej) => {
            res('OK')
        })
    }
    async function main2() {
        throw '这是throw'
    }

    console.log(main())
    console.log(main1())
    console.log(main2())
```

![1646116252952](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646116252952.png)

##### await表达式

1. await右侧表达式一般为promise对象，但也可以是其他的值
2. **如果表达式是promise对象，await返回的是promise成功的值**
3. 如果表达式是其他值，直接将**此值作为await的返回值**
4. 注意！！：await必须写在async函数中，但async函数中可以没有await
5. 如果await的promises失败了，就会抛出异常，需要通过try,,,catch捕获处理。

```js
async function hello() {
    let p1 = new Promise((res, rej) => {
        res('OK')
    })
    let p2 = new Promise((res, rej) => {
        rej('fail')
    })

    //1.右侧为promise
    let r1 = await p1

    //2.右侧为其他类型的值
    let r2 = await 20

    try {
        //3.右侧为失败的promise，需要捕获
        let r3 = await p2
        } catch (e) {
            console.log(e) //失败的结果
        }

    console.log(r1)
    console.log(r2)

}
```

##### 结合await和async

**读取 三个文件的场景**

```js
const req = require('express/lib/request')
let fs = require('fs')
const util = require('util')
const minReadFile = util.promisify(fs.readFile)

async function main() {
    try { //读取第一个文件的内容
        let data1 = await minReadFile('1.txt')
        let data2 = await minReadFile('2.txt')
        let data3 = await minReadFile('3.txt')
        console.log(data1 + data2 + data3)
    } catch (e) {
        console.log(e)
    }

}

main()
```

**发送ajax请求**

```js
function sendAjax(url) {
    return new Promise((res, rej) => {
        let xhr = new XMLHttpRequest()
        xhr.open('get', url)
        xhr.send()
        xhr.onreadystatechange = function() {
            if (xhr.readyState == 4) {
                if (xhr.status >= 200 && xhr.status < 300) {
                    res(xhr.responseText)
                } else {
                    rej('服务器坏了')
                }
            }
        }
    })

}

setTimeout(async function() {
    let result = await sendAjax('http://localhost:8001/ajax_promise')
    console.log(result)
}, 1000)
```



### 2.14 Set

ES6提供了新的数据结构Set集合。它类似于数组,值是唯一的去重，但成员的值都是唯一的，集合**实现了iterator接口**，所以**可以使用扩展运算符和for..of进行遍历**，集合的属性和方法：

1. size	返回集合的元素个数
2. add	增加一个新元素，返回当前集合
3. delete	删除元素，返回boolean值
4. has	检测集合中是否包含某个元素，返回boolean值
5. clear	清空集合，返回undefined

```js
let s = new Set()

let s2 = new Set(['刘强', '我去', '刘强', '吴云'])
console.log(s2) //Set(3) {'刘强', '我去', '吴云'}
console.log(s2.size) //3

s2.add('俞文竹')
console.log(s2)//Set(4) {'刘强', '我去', '吴云', '俞文竹'}

s2.delete('我去')
console.log(s2)//Set(3) {'刘强', '吴云', '俞文竹'}



console.log(s2.has('俞文竹'))//true
console.log(s2.has('狗比'))//false

for (let v of s2){
    console.log(v)
}

s2.clear()
console.log(s2)//Set(0) {size: 0}
```

#### 集合实践

##### 数组去重

```js
let arr = [1,2,2,3,3,4.5,6,6,7]
let result = [...new Set(arr)]
console.log(result)  //[1, 2, 3, 4.5, 6, 7]
```

##### 交集

```js
let arr1 = [1, 2, 2, 3, 3, 4.5, 6, 6, 7]
let arr2 = new Set([2, 3, 4.5, 6])

let result1 = [...new Set(arr1)].filter(item => arr2.has(item))

console.log(result1) // [2, 3, 4.5, 6]
```

##### 并集

```js
let union = [...new Set([...arr1, ...arr2])]
console.log(union)
```

##### 差集

```js
let arr1 = [1, 2, 2, 3, 3, 4.5, 6, 6, 7]
let arr2 = new Set([2, 3, 4.5, 6])

let result1 = [...new Set(arr1)].filter(item =>! arr2.has(item))

console.log(result1) // [1, 7]
```

### 2.15 Map

ES6提供了Map数据结构。它**类似于对象，也是键值对的结合**。但是'健'的范围不限于字符串，**各种类型的的值(包括对象)都可以当作键**。Map实现了iterator接口，所以可以**使用扩展运算符和和for...of**进行遍历。Map的属性和方法。

1. size	返回Map的元素个数
2. set	增加一个新元素，返回当前Map
3. get	返回键名对象的键值
4. has	检测Map中是否包含某个元素，返回boolean值
5. clear	清空Map，返回undefined

```js
let m = new Map()

m.set('name', '刘强')
m.set('age', 24)
m.set('change', function() {
    console.log('change')
})

console.log(m.size) //3

let key = {
    school: '南昌大学'
}

m.set(key, ['江西', '南昌'])
console.log(m) //Map(4) {'name' => '刘强', 'age' => 24, 'change' => ƒ, {…} => Array(2)}

m.delete(key)
console.log(m) //Map(3) {'name' => '刘强', 'age' => 24, 'change' => ƒ}

console.log(m.get('name')) //刘强

m.clear()
```

### 2.16 class类

 ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念， 作为对象的模板。通过class关键词，可以定义类。基本上， ES6 的 class 可以看作只是 一个语法糖，它的绝大部分功能，ES5 都可以做到，新的 class 写法只是让对象 原型的写法更加清晰、更像面向对象编程的语法而已。  

#### class声明类

```js
//es5构造函数
function Stu(name, age) {
    this.name = name
    this.age = age
}

Stu.prototype.read = function() {
    console.log('读书')
}

let liu = new Stu('刘强', 25)
console.log(liu)



//class声明
class Stu {
    //构造方法 名字不能修改
    constructor(name, age) {
        this.name = name
        this.age = age
    }

    //方法必须使用改语法 不可以使用es5
    read() {
        console.log('读书')
    }
}
let yu = new Stu('俞文竹', 25)
yu.read()
```

#### class静态成员

给函数添加属性，实例对象接收不到的！

![1645669967519](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645669967519.png)

同样class 也可以 可以使用class静态属性。

**静态属性 属于类 不属于实例对象**

```js
class Stu {
    //构造方法 名字不能修改
    constructor(name, age) {
        this.name = name
        this.age = age
    }

    static school = '南昌大学'
    static food = () => {
            console.log('最爱吃都蟹煲')
        }
        //方法必须使用改语法 不可以使用es5
    read() {
        console.log('读书')
    }
}


let yu = new Stu('俞文竹', 25)
Stu.food() //最爱吃都蟹煲
yu.food()//报错
```

#### 继承

##### ES5构造函数继承

```js
function Stu(name, age) {
    this.name = name
    this.age = age
}

Stu.prototype.read = function() {
    console.log('读书')
}

function Yjs(name, age, school, score) {
    Stu.call(this, name, age)
    this.school = school
    this.score = score
}
Yjs.prototype = new Stu;
Yjs.prototype.construtor = Yjs

Yjs.prototype.shangxue = function() {
    console.log('我可以上学了')
}

Yjs.prototype.scores = function() {
    console.log('我有分数了')
}

let s = new Yjs('俞文竹', 25, '南昌大学', 78)
console.log(s)
```

##### class类的继承

```js
class Stu {
    constructor(name, age) {
        this.name = name
        this.age = age
    }
    read() {
        console.log('读书')
    }
}

class Yjs extends Stu {
    constructor(name, age, school, score) {
        super(name, age)
        this.school = school
        this.score = score
    }

    hangxue() {
        console.log('我可以上学了')
    }

    scores() {
        console.log('我有分数了')
    }
}
let s = new Yjs('俞文竹', 25, '南昌大学', 78)
console.log(s)
```

##### 子类对父类方法的重写

```js
class Stu {
    read() {
        console.log('读书')
    }
}

class Yjs extends Stu {
    read() {
        console.log('yjs读书')
    }

}

let s = new Yjs()
s.read() //js读书
```

#### getter和setter

```js
class Stu {
    get score() {
        console.log('分数出来了')
        return '86分！'
    }
    set score(scores) {
        console.log('输入分数:', scores)
    }

}

let s = new Stu()
s.score = 99
console.log(s.score)
```

### 2.17 数值扩展

Number.EPSILON是js表示的最小精度

```js
console.log(Number.EPSILON)//2.220446049250313e-16

console.log(0.1 + 0.2 === 0.3)  //0.30000000004 不等于0.3 false


function equal(a, b) {
    if (Math.abs(a - b) < Number.EPSILON) {
        return true
    } else {
        return false
    }
}

console.log(equal(0.1 + 0.2, 0.3)) true
```

#### 二进制和八进制

```js
let b = 0b1010 二进制
let o = 0o777 八进制
let d = 100 十进制
```

#### Number.isFinite()和Number.isNaN

 Number.isFinite() 用来检查一个数值是否为有限的 

```js
Number.isFinite(100)
//true
Number.isFinite(100/0)
//false
Number.isFinite(Infinity)
//false
```

Number.isNaN() 用来检查一个值是否为 NaN  

```js
Number.isNaN(12)
//false
Number.isNaN('s'*12)
//true
```

#### Number.parseInt()和Number.parseFloat()

 ES6 将全局方法 parseInt 和 parseFloat，移植到 Number 对象上面，使用不变。  

```js
Number.parseInt('1231s')//1231
Number.parseFloat('12312.2323asd')//12312.2323
```

#### Math.trunc

```js
Math.trunc(1.34)//1
```

#### Number.isInteger 

 Number.isInteger() 用来判断一个数值是否为整数 

```js
Number.isInteger(2)
//true
Number.isInteger(2.0)
//true
Number.isInteger(2.1)
//false
```

### 2.18 对象扩展

ES6新增了一些Object对象的方法

#### Object.js

比较两个值是否严格相等，与===行为基本一致(NaN除外)

```js
Object.is(100,100) // true
Object.is(NaN,NaN) //true
NaN ===NaN//false
```

#### Object.assign

对象的合并，将元对象的所有可枚举属性，复制到目标属性

```js
let stu = {
    name: '学生姓名',
    age: '学生年龄',
    school: '学生学校',
    sex: '男'
}

let liu = {
    name: '刘强',
    age: 25,
    school: '南昌大学',
}

Object.assign(stu, liu) //{name: '刘强', age: 25, school: '南昌大学', sex: '男'}
```

#### 设置原型对象

\__proto\__、setPrototypeOf、getPrototypeOf可以直接设置对象的原型

```
const school = {
    name: '南昌大学'
}

const cities = {
    city: ['南昌', '合肥']
}
Object.setPrototypeOf(school, cities)
```

![1645692527870](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645692527870.png)

![1645692731234](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645692731234.png)

### 2.19 模块化

模块化是将一个打的程序文件，拆分成多小的文件，然后将小文件组合起来

#### 模块化好处

1. 防止命名冲突
2. 代码复用
3. 高维护性 

#### 模块化规范产品  

 ES6 之前的模块化规范有： 

1) CommonJS => NodeJS、Browserify 

2) AMD => requireJS 

3) CMD => seaJS  

#### 模块化语法

模块功能主要由两个命令构成：export和import.

- export命令用于规定模块的对外接口

  ```js
  let name = '刘强'
  
  function read() {
      console.log('你好')
  }
  
  export { name, read }
  ```

- import命令用于输入其他模块提供的功能

  ```js
  <script type="module">
      import * as m1 from './m1.js'; 
  	console.log(m1.name)
  	console.log(m1.read())
  </script>
  ```

#### 暴露模块方式

**分别暴露**

```js
export let name = '刘强'

export function read() {
    console.log('你好')
}
```

**统一暴露**

```js
let name = '刘强'

function read() {
    console.log('你好')
}
export { name, read }
```

**默认暴露**

```js
export default {
    name,
    read1 = () => {
        console.log('你好')
    }
}
```

#### 引入模块方式

**通用暴露方式**

```js
import * as m1 from './m1.js'; 
console.log(m1.read())
```

**结构赋值形式**

同名和default可以 用as

```js
 import {read,name} from './m1.js'; 
 import {read as read2,  name} from './m1.js'; 
import {default as m3} from './m1.js'
```

**简便形式**

只针对默认暴露

```js
 import read  from './m1.js'; 
```

**总体引入模块**

index.js

```js
import * as m1 from './m1.js'
import * as m2 from './m2.js'
console.log(m1);
console.log(m2);
```

index.html

```js
<script src="index.js" type="module"></script>
```

### babel转换es6

1.安装 babel-cli 	babel-preset-env 	browserify(webpack)

```js
npm i babel-cli  babel-preset-env 	browserify -D
```

2.开始转换

```js
 npx babel ./ -d  ./dist/js --presets=babel-preset-env
```

3.打包

```js
npx browserify dist/js -o dist/bundle.js 
```

4.引入文件

```js
<script src="dist/bundle.js"></script>
```
