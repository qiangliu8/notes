# Node.js

[TOC]

## 一、模块化

1. 在Node中，**一个js文件就是一个模块。**
2. 在node中，每一个js文件的js代码都是独立运行在一个函数中，而不是全局作用域，所以**一个模块中的变量和函数在其他模块中无法访问**。

### 暴露属性

**我们可以通过exports来向外部暴露变量和方法**

只需要将需要暴露的属性和方法设置为exports的属性就可以。

```js
console.log('我是模块1的打印')
let a =100 //对外部来说不可见
let name = '我是1.js'

//向外部暴露属性
exports.name = name
//module.exports.name = name 一样的
exports.sayHello = () => {
    console.log('1.js暴露的方法')
}
```

### 引入属性

**在node中，通过require()函数来引入外部的模块**

1. require()可以传递一个文件的路径作为参数，node会自动根据该路径来引入外部的路径，必须以.或者..开头
2. 使用require()引入模块以后，该函数会返回一一个对象那个，这个的对象代表的就是引入的模块。
3. 我们使用require()引入外部模块时，使用的就是模块标识，我们可以通过模块表示来找到指定的模块。

```js
var md = require('./1.js')

console.log(md.sayHello())
```

### 模块分类

模块分成两大类

- **核心模块**

  由node引擎提供的模块

  核心模块的表示就是模块的名字

  ```js
  var fs = require('fs')
  ```

- **文件模块**

  由用户自己创建的模块

  ```js
  var fs = require('./fs.js')
  ```

  

### global属性

在node中有一个全局对象global，他的作用和winows类似

在全局中创建的变量都会作为global的属性保存

在全局中创建的函数都会作为global的方法保存

**但是必须去掉var let**

```js
name1 = '1'
let name2 = '2'

console.log(global.name1) //1
console.log(global.name2) //undefined

console.log(arguments.callee + '')
```

### 模块化详解！！ 

arguments.callee这个属性保存的是当前执行的函数对象

打印出来后的结果就是

```js
function (exports, require, module, __filename, __dirname) {
name1 = '1'
let name2 = '2'

console.log(global.name1) //1
console.log(global.name2) //undefined

console.log(arguments.callee + '')
}
```

当node在执行模块的代码时，它会首先在代码的最顶层，添加如下代码

```js
function (exports, require, module, __filename, __dirname) {
```

在代码的最顶层，添加如下代码

```js
}
```

所以哦！！！**实际上模块中的代码都是包装在一个函数中执行的，并且在函数执行时，同时传递了5个实参！**

1. **exports**

   该对象用来将变量或函数暴露到外部

2. **require**

   函数：用来引入外部的函数

3. **module**

   module代码表当模块本身

   exports就是modules的属性

   ```js
   console.log(module.exports === exports) //true
   ```

4. **__filename**

   当前模块的完整路径

5. **__dirname**

   当前模块所在文件夹的路径

#### exports和module.exports

**通过exports只能通过.的方式向外暴露内部变量**

exports.xxx = ...

**module.exports既可以通过.的形式，也可以直接赋值**

module.exports.xxx =....

module.exports.={}

因为exports={}错了直接相当于清空了对象

## 二、包

![1645795009891](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645795009891.png)

![1645795018248](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645795018248.png)

## 三、Buffer缓冲区

### Buffer缓冲区

1. Buffer的结构和数组很像，操作的方法也和数组类似。
2. 数组中不能存储二进制文件，**Buffer专门用来存储二进制文件。**
3. 在Buffer中不需要引入模块，**直接引入**就可以
4. 在Buffer中存储的都是二进制，用16进制显示。所以buffer每一个伊苏的范围是从0-ff 0-255。buffer中的一个元素，占用内存的一个字节。
5. **Buffer的大小一旦确定，不可修改**

```js
 var str = 'hello 尚硅谷'

//将一个字符串保存到buffer中
var buf = Buffer.from(str)
console.log(buf) //<Buffer 68 65 6c 6c 6f 20 6e 6f 64 65>
console.log(buf.toString()) //hello node 


console.log(buf.length) //15 这是占用内存的大小
console.log(str.length) //9 这是字符串的长度
```

**new Buffer(size)创建一个指定大小的buffer**

Buffer所有构造函数都废弃了

```js
var buf2 = new Buffer(10) //10个字节的buffer
```

 **使用alloc(size)创建buffer**

```js
var buf3 = Buffer.alloc(10)
buf3[0] = 88
buf3[1] = 0xaa
console.log(buf3)
//<Buffer 58 aa 00 00 00 00 00 00 00 00>


//只要数字在控制台页面输出，一定是10进制,
//不是数字的化可以用toString
console.log(buf3[0]) //88
console.log(buf3[0].toString(2)) //1011000
```

**使用allocUnsafe(size)创建buffer**

```js
//allocUnSafe可能含有敏感数据，就是上一个内存未清空
//只分配空间，不清空数据。
var buf4 = Buffer.allocUnSafe(10)

console.log(buf4) //<Buffer 00 00 00 00 00 00 00 00 00 00>
```

![1645862205668](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645862205668.png)

![1645862154464](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645862169517.png)

![1645862215627](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645862215627.png)

## 四、文件系统

文件系统简单来说就是通过node操作系统的中的文件

 服务器的本质就将本地的文件发送给远程的客户端。

使用文件系统，需要引入fs模块，fs是核心模块，不需要下载直接引入。

![1645862462421](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645862462421.png)

异步都有callback参数

### 同步文件写入

1. 打开文件

   **fs.openSync(path, flags,mode) **

     path 要打开的文件路径

     flags 操作类型 r只读 w可写

     mode 设置文件的操作权限，一般不传

   返回值：该方法会返回一个文件的描述符作为结果，我们可以通过该描述符来对文件进行各种操作。

2. 写入文件

   **fs.writeSync( fd, String，position，encoding)**

   fd 文件描述符，需要传递要写入的文件的描述符

   string 要写入的内容

   position 写入的起始位置

   ecoding 写入的编码，默认utf-8

3. 关闭文件

   **fs.closeSync(fd)**

   fd 文件描述符

```js
//1.引入fs模块
const fs = require('fs')
//2.打开文件
var f = fs.openSync('1.txt', 'w')
//3.写入文件
fs.writeSync(f, '今天天气真不错')
//4.关闭文件
fs.closeSync(f)
```

### 异步文件写入

1. 打开文件

   **fs.openSync(path, flags,mode，callback) **

     path 要打开的文件路径

     flags 操作类型 r只读 w可写

     mode 设置文件的操作权限，一般不传

     callback 结果都是通过回调函数返回

   返回值：该方法会返回一个文件的描述符作为结果，我们可以通过该描述符来对文件进行各种操作。

2. 写入文件

   **fs.writeSync( fd, String,position,encoding,callback)**

   fd 文件描述符，需要传递要写入的文件的描述符

   string 要写入的内容

   position 写入的起始位置

   ecoding 写入的编码，默认utf-8

3. 关闭文件

   **fs.closeSync(fd,callback)**

   fd 文件描述符

```js
//1.引入fs模块
var fs = require('fs')
    //2.打开文件
fs.open('1.txt', 'w', (err, fd) => {
    if (!err) {
        //3.写入文件
        fs.write(fd, '我想去晒被子', (err) => {
            if (!err) console.log('写入成功')
                //4.关闭文件
            fs.close(fd, err => {
                if (!err) console.log('关闭成功')

            })
        })
    } else {
        console.log(err)
    }
})
```

### 简单文件写入

![1645866613568](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645866613568.png)

```js
var fs = require('fs')

fs.writeFile('2.txt', '我想睡觉', { flag: 'w' }, (err, data) => {
    if (!err) {
        console.log('写入成功')
    }
})
```

![1645866722603](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645866722603.png)

### 流式文件写入

同步、异步、简单写入都不适合大文件的写入，性能较差，，容易导致内存溢出。这时候需要流失文件写入。

  – fs.createReadStream(path[, options])

  • path 文件路径

  • options {encoding:"",mode:"",flag:""}

```js
var fs = require('fs')
//创建一个可写流
var ws = fs.createWriteStream('3.txt')

//可以通过流的open和close时间来监听流的打开和关闭。
ws.once('open', function() {
    console.log('流打开了')
})
ws.once('close', function() {
    console.log('流关闭了')
})
//通过ws向文件中输入内容 可以分多次
ws.write('111')
ws.write('222')
ws.write('333')

//关闭流
ws.end()
//ws.close()  回执行一部分
```

### 简单文件读取

![1645878981317](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645878981317.png)

```js
var fs = require('fs')

fs.readFile('wenwen.png', (err, data) => {
    if (!err) {

        fs.writeFile('温温.png', data, err => {
            console.log('写入成功！')
        })
    }
})
```

### 流式文件读取

![1645879455459](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645879455459.png)

```js
var fs = require('fs')

var rs = fs.createReadStream('wenwen.png')
var ws = fs.createWriteStream('wenwen1.png')

rs.once('open', function() {
    console.log('可读流打开了')
})

rs.once('close', function() {
    console.log('可读流流关闭了')
    ws.end()  !!!!!注意!!!!! 在这里关闭可写流
})

ws.once('open', function() {
    console.log('可写流打开了')
})

ws.once('close', function() {
    console.log('可写流关闭了')
})

//如果要读取一个可读流的数据，必须要为可读流绑定一个data事件，data事件绑定完毕，它就自动开始读取数据
rs.on('data', function(data) {
    ws.write(data)
})


```

可以使用管道！

```js
var fs = require('fs')

var rs = fs.createReadStream('wenwen.png')
var ws = fs.createWriteStream('wenwen1.png')

rs.once('open', function() {
    console.log('可读流打开了')
})

rs.once('close', function() {
    console.log('可读流流关闭了')
})

ws.once('open', function() {
    console.log('可写流打开了')
})

ws.once('close', function() {
    console.log('可写流关闭了')
})

//可以将可读流中内容直接写入到可写流中
rs.pipe(ws)
```

### 其他操作

![1645880960759](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645880960759.png)

![1645880971792](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645880971792.png)

![1645880978120](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1645880978120.png)