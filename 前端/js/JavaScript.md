[TOC]



# JavaScript基础

1. js严格区分大小写
2. 分号结尾
3. JS中会忽略多个空格和换行，所以我们可以利用空格和换行对代码进行格式化



## 一、数据类型

js中共有六种数据类型

- **String** 字符串
- **Number** 数值
- **Boolean** 布尔值
- **Null** 空值
- **Undefind** 未定义
- **Object** 对象

String、Number、Boolean、Null、Undefind、Object属于**基本数据类型**，Object属于**引用数据类型**



### Number

##### Infinity

**Number.MAX_VALUE**=1.7976931348623157e+308

如果使用Number表示超过了最大值，则会返回一个Infinity

​	**Infinity表示正无穷**

​	**-Infinity表示负无穷**

使用typeof检查Infinity也会返回Number

##### NAN

NaN是一个特殊的数字，表示Not a Number

使用typeof检查NaN也会返回Number

#### 注意

如果使用JS进行浮点元素计算，可能会得到一个不精确的结果

所以千万不要使用JS进行精确度要求比较高的运算

```javascript
var c = 0.1+0.2
console.log(c); //0.300000005
```

### 强制类型转换

#### String转换

指将一个数据类型强制转换成其他的数据类型

类型转换主要指，将其他的数据类型，转换为 String Number Boolean

```
var a = 123
a.toString()
```

##### 方法一toString()

 调用被转换数据类型的tgString()方法

该方法不会影响到原变量，它会将转换的结果返回

但是注意:**null和undefined这两个值没有toString **如果调用他们的方法，会报错

```
var a = 123
a.toString()
```

##### 方法二String( )

调用String( )函数，来将被转换的数据作为参数传递给函数

使用String( )函数做强制类型转换时，

​		**对于Number和Boolean实际就是调用的toString()方法**

​		**对于Null和underfind，就不会调用toString( )方法。**

​				**他会将null 和underfind自动转换成“underfind”**

null和undefined也可以调用了

```
var a = 123
String(a)
```

#### Number转换

 同理Number，

##### 方法一Number( )

使用Number( )函数

1. 字符串-->数字
   1. 如果是纯数字的字符串，则直接转换成数字
   2. 如果字符串中**有非数字的内容，则转换成NAN**	
   3. 字符串是**空串或空格，则转换成0**
2. 布尔-->数字
   1. true 转成1
   2. false转成0
3. Null -->数字0
4. underfind转成NAN	

##### 方法二parseInt( )

将**字符串中有效整数内**容取出来，然后转换成Number

parseInt(a.10) 采用十进制转换

##### 方法三parseFloat( )

将**字符串中有效内容包括小数**取出来，然后转换成Number

#### Boolean转换

使用Boolean( )

1. 数字-->布尔 **除了0和NAN，其余都是true**
2. 字符串-->布尔 **除了空串，其余都是true**
3. null-->布尔 **都是false**
4. underfind-->布尔 **都是false**
5. object也会转换成true

### 基本数据类型和引用数据类型的区别

**基本数据类型**

String Number Boolean Null underfind

**引用数据类型**

Object



JS中的变量都是保存到栈内存中的，

- 基本数据类型的值直接在**栈内存中存储**，互不影响。

  ![image-20211124111542678](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211124111542678.png)

- 对象是保存在堆内存中，每创建一个新对象，就会在堆内存中开辟一个新的空间。

  而**变量保存的是对象的内存地址**（对象的引用。）

  ​		![image-20211124111515566](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211124111515566.png)

## 二、运算

### +

- **任何值和NaN做运算都是NAN**

- 当对非Number类型的值进行运算时，会将这些值转换为Number

- 两个字符串相加，会拼串

- **任何和字符串相加的其余数  ，会首先转换成字符串，**再拼串

  - ```javascript
    var c = 123
    c = c + “”
    var a = "123"
    a = a - 0 
    //c就变成字符串，a变成数字，属于隐式转换
    ```

- 计算顺序从左到右

  - ```javascript
    result = 1 + 2 + “3”  //"33"
    result = "1" + 2 + 3  //"123"
    ```

    

### -    *

非字符串不会转换成字符串

```
result = 100 -true //99
result = 100 -"1" //99
result = 2 * "8" //16
result = 2 - underfind //2-NAN = NAN
```



### 比较

##### 布尔 null underfind

首先转换为数值型在进行比较

##### NAN

任何和NAN相比都是false

##### 字符串

两个字符串比较时，比较的是字符串的**字符编码**，字符编码是**一位一位**进行比较。

注意在比较两个字符串型的数字时，要记得转型。加一个+号



#### ==

- 使用==来比较两个值时，**如果值的类型不同。则会自动进行类型转换**，将其转换为相同的类型，然后再进行比较。
- null==0 ，为false
- underfind 衍生自null，所以 二者相等
- NaN不和任何值相等，包括他本身.所以只能用isNaN()来判断使得否是NAN

#### ===

全等不会做类型转换

### 运算优先级

![image-20211122202424908](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211122202424908.png)

## 三、代码块

代码块内容，在外部是完全可见的。

```javascript
{
    var s = 1
}
console.log(s) /
```

## 四、对象

### 创建对象

使用new关键字调用的函数，是**构造函数constructor**

```js
var obj = new Object()
```

使用对象自变量来创建一个对象,可以直接指定对象中的属性

```js
var obj  = {}
var obj1  = {name:'liuqiang '}
```

#### 工厂模式

使用工厂方法创建对象

```js
function createObject(name, age, gender) {
    let obj = new Object()
    obj.name = name
    obj.age = age
    obj.gender = gender
    obj.sayHello = function() {
        console.log(`${obj.name}今年${obj.age}岁，性别${obj.gender}`)
    }
    return obj
}

let liu = createObject("刘强", 24, '男')

liu.sayHello()
```

#### 构造函数

创建一个构造函数，专门用来创建Person对象的

构造函数就是一个普通的函数，创建方式和普通函数没有区别不同的是构造函数习惯上首字母大写

```js
function Person(name) {
    this.name = name
    this.sayName = function() {
        console.log(this.name)
    }
}

var p = new Person("liuqiang")
p.sayName()
```

**构造函数优化**

这样不会一直创建函数

```js
function sayName(){
    console.log(this.name)
}
function Person(name) {
    this.name = name
    this.sayName = sayName
}

var p = new Person("liuqiang")
p.sayName()
```



### 删除对象属性

```js
delete obj.name
```

### 检查属性

#### in 运算符

通过该运算符可以检查一个对象中**是否含有指定的属性**，如果有则返回true，反之返回false

如果本身没有，原型有则也返回true

语法：属性名 in 对象

```js
console.log("name" in obj)
```

#### hasOwnProperty()

可以使用对象的hasOwnProperty()来检查对象自身中是否含有该属性使用该方法

只有当对象**自身中含有属性时**，才会返回true

#### 枚举对 象

for  .... in

```javascript
for(var n in obj){
	console.log(n) //n为对象的属性名
	console.log(obj[n])//对象的属性值
}
```

#### instanceof

使用instance可以检查一个对象是一个类的实例

**任何对象都是Object的实例**

```javascript
对象 instanceof 构造函数
```

### 原型对象prototype

- **我们所创建的每一个函数，解析器都会向函数中添加一个属性prototype**.

  这个属性对应着一个对象，这个对象就是我们所谓的原型对象

- 如果函数作为普通函数，则prototype对象没作用

- 当函数以构造函数的形式调用时，它所创建的对象中都会有一个隐含的属性，

  指向该构造函数的**原型对象**，我们可以通过**\_proto\_来**

- 原型对象就相当于一个公共的区域，所有同一个类的实例，都可以访问到这个原型对象，我们可以将对象中共有的内容 ，统一设置到原型对象中。

  ```javascript
  function MyClass(name) {
      this.name = name
  }
  
  //向原型中添加name
  MyClass.prototype.sayName = function() {
      console.log(this.name)
  }
  
  var o1 = new MyClass("o1")
  o1.sayName() //o1
  var o2 = new MyClass("o2")
  o2.sayName()//o1
  
  o1._proto_ = MyClass.prototype
  ```

  函数.prototype == 对象.__proto__

  

## 五、函数

**使用函数声明创建函数**

```js
function 函数名([形参1,形参2,,,,,形参N]){
	语句
}
```

**使用函数表达式创建函数**

```js
var fun = function([形参1,形参2,,,,,形参N]){
	语句
}
```

#### 立即执行函数

立即执行，只执行一次

```js
(function(a,b){
	console,log(a+b)
})(1,2)
```

## 六、作用域

作用域指的是一个变量的作用的范围

### 全局作用域

- 全局作用域在页面打开时创建，在页面关闭时销毁。

- 在全局作用域中有一个全局对象window，它代表一个浏览器的窗口。由浏览器创建直接使用。

  **在全局作用域中，创建的变量都会作为winow对象的属性保存。**

  **在全局作用域中，创建的函数都会作为winow对象的方法保存。**
  
  ```javascript
  var num = 123
  console.log(window.num)//123
  ```
  
  

#### 变量的声明提前

使用var 关键字声明的变量，会在所有的代码**执行之前被声明（不会赋值）。**

​	但是如果声明变量时不适用var,则不会被提前

```javascript
<script>
	console.log(a)//不会报错，会打印underfind
	var a =123;
</script>
```

#### 函数的声明提前

使用函数声明形式创建的函数 function 函数(){}

​		它会在所有代码执行之前就被创建，所以我们可以在函数声明前来调用函数

使用函数表达式创建的函数，不会被声明提前，所以报错。

```javascript
<script>
	fun1()//123
	fun2()//报错
	
	function fun1(){
		console.log(123)			//放在那里都可以
	}
	var fun2 = function(){
		console.log(123)
	}
</script>
```

### 函数作用域

- 调用函数时创建函数作用域，函数执行完毕之后，函数作用域销毁

- 每调用一次函数就会创建一个新的函数作用域，他们之间是互相独立的。

- 函数作用域中可以访问到全局作用域的变量，反之全局不可访问函数内部

- 当在函数作用域操作一个变量时，它会先在自身作用域中寻找，如果有就直接使用。

  ​	如果没有则向上一级作用域中寻找，直到找到全局作用域，

  ​	如果全局作用域中依然没有找到，则会报错ReferenceError

- 在函数中可以使用window对象访问全局变量

### this关键字

解析器在调用函数每次都会向函数内部传递一个隐含的参数

这个隐含的参数就是this，this指向的是一个对象，这个对象我们称为函数执行的上下文对象。

根据函数的调用方式的不同，this会指向不同的对象。

1. **以函数调用时，this永远都是window对象**

   ```javascript
   var name = "全局"
   
   function fun() {
       console.log(this.name)
   }
   
   fun() //全局
   
   
   function f1(){
       function f2(){
           console.log(this)
       }
       f2()
   }
   f1() //全局
   ```

2. 当以方法的形式调用时，谁调用方法this就是谁

   ```javascript
   var o1 = {
       name: "o1",
       callname: fun
   }
   
   var o2 = {
       name: "o2",
       callname: fun
   }
   
   o1.callname() //o1
   o2.callname() //o2
   ```

3. 当以构造函数的形式调用时，this就是新创建的那个对象

   ```javascript
   function Person(name) {
       this.name = name
       this.sayName = function() {
           console.log(this.name)
       }
   }
   
   var p = new Person("liuqiang")
   p.sayName()
   ```

4. 使用通过call和apply调用时，this是指定的参数的对象

### call和apply

这两个 方法都是函数对象的方法，需要通过函数对象来调用

当对函数调用call和apply都调用函数执行

```javascript
function fun() {
    console.log("我是fun函数")
}

fun.call()//我是fun函数
fun.apply()//我是fun函数
```

在调用call和apply可以将一个对象指定为第一个参数，此时**这个对象将会成为函数执行的this**。

```javascript
function fun() {
    console.log(this.name)
}

var obj1 = {
    name: "刘强",
    sayName:function(){
        console.log(this.name)
    }
}
var obj2 = { name: "俞文竹" }

fun.call(obj1)//刘强
fun.apply(obj2)//俞文竹
obj1.sayName.call(obj2)//俞文竹
```

call方法可以将实参**在对象之后依次传递**

apply()方法需要将实参封装到**一个数组中统一传递**

```javascript
function fun1(a, b) {
    console.log(a)
    console.log(b)
}
fun1.call(obj1, 1, 2) //1,2
fun1.apply(obj1, [1, 2])//1,2
```

### argument参数

在调用函数时，浏览器每次都会传递进两个隐含的参数：

1. **函数的上下文对象this**
2. **封装实参的对象 arguments。**
   - 它是一个类数组对象，它也可以通过索引来操作数据，也可以获取长度
   - 在调用函数时，我们所传递的实参都会在argument中保存
   - arguments还有一个**callee**的属性，它对应一个函数对象，就是当前正在指向的函数的对象

```javascript
function fun() {
    console.log(arguments.length)
    console.log(arguments[0])
    console.log(arguments.callee == fun)
}

fun(123,456) //2  123
```

## 七、垃圾回收

当一个对象没有任何变量和属性对它进行引用，此时我们将永远无法操作该对象，此时这个对象就是一个垃圾。对象过多时，会占用大量内存。

```javascript
var obj = new Object();
obj = null
```

浏览器会自动回收。

## 八、数组

### 数组方法

#### push

该方法可以向数组的末尾添加一个或多个元素，并返回数组的长度。**会改变原数组**

```javascript
var arr = new Array()
r = arr.push(123) //1
r = arr.push(456) //2
console.log(arr)  //Array(2)
```

#### unshift()

该方法可以向数组的开头添加一个或多个元素，并返回数组的长度。**会改变原数组**

```javascript
var arr = new Array()
r = arr.unshift(456) //1
r = arr.unshift(123) //2
console.log(arr)  //Array(2) 123，456
```

#### shift()

该方法可以向数组的开头删除一个元素 ，并返回被删除元素。**会改变原数组**

```javascript
var arr = new Array()
arr.push(123)
arr.push(456)//1
console.log(arr.shift())  //123
console.log(arr) //456
```

#### pop

该方法可以向数组的末尾删除一个元素 ，并返回被删除元素。**会改变原数组**

```javascript
var arr = new Array()
arr.push(123) //1
console.log(arr.pop())  //123
console.log(arr) //没有
```

#### slice和splice

**sclice()**可以从数组中提取元素、返回截取内容，**不会改变原数组**

参数:	

1. 截取开始的位置的索引
2. 截取结束的的位置的索引，可以省略不写时，截取到 末尾

**splice()**可以从数组中删除元素、返回删除内容，**会改变原数组**

参数:	

1. 截取开始的位置的索引
2. 删除的数量

#### concat()

concat()可以连接两个或多个数组，并将新的数组返回。**不会改变原数组。**

```javascript
var arr1 = [1,2,3]
var arr2 = [4,5,6]
console.log(arr1.concat(arr2))
```

#### join()

该方法可以将数组转换为一个字符串。**不会改变原数组。**返回字符串

指定一个字符串作为参数，作为连接符

```javascript
var arr3 = ['我','是','刘强']//我是刘强
```

#### reverse()

反转数组，会改变原数组

#### sort()

对数组元素进行排序，**会改变原数组**，默认按照unicode编码进行排序，即使数字数组，也会默认unicode

所以我们需要指定排序规则：

我们可以在sort中添加一个回调函数，来指定排序规则。回调函数中需要定义两个形参，根据函数方法调用实参去确定。根据元素返回值确定交换位置。

```javascript
var arr4 = [2,1,3]
arr.sort(function(a,b){
	return a>b?1:-1
})
```

秒

```javascript
//升序
arr.sort(function(a,b){
    return a-b
})
//降序
arr.sort(function(a,b){
    return b-a
})
```

### 字符串的方法

在底层字符串是以**字符数组的形式**保存的

**lenth属性**

可以用来获取字符串的长度

``` javascript
var str = "liuqiang"
console.log(str.length) //8
console.log(str[0]) //l
```

**charAt()**

可以返回字符串中指定的位置的字符

根据索引获取指定字符

``` javascript
var str = "liuqiang"
console.log(str.charAt(0)) //l
```

**charCodeAt()**

可以返回字符串中指定的位置的字符unicode编码

``` javascript
var str = "liuqiang"
console.log(str.charCodeAt(0)) //l08
```

**fromCharCode()**

可以根据字符编码去获取字符

``` javascript
console.log(String.fromCharCode(108)) // l
```

**concat()**

可以用来链接两个或多个字符串

``` javascript
var str = "liuqiang"
console.log(str.concat("love","yuwenzhu"))//liuqiangloveyuwenzhu
```

**indexOf()**

该方法可以检索一个字符串中是否含有指定内容

如果字符串中含有该内容，则会返回其第一次出现的索引

指定第二个参数，作为参数查找的位置

``` javascript
var str = "liuqiang"
console.log(str.indexOf("l"))//0
console.log(str.indexOf("i",3))//4
```

**lastIndexOf()**

用法差不多 ，这个是从后往前、

**slice()**

可以从字符串中，截取指定的内容。

参数;

第一个:开始截取位置的索引(包括开始位置)-

第二个:结束位置的索引（不包括结束位置)

``` javascript
var str = "liuqiang"
console.log(str.slice(0,2))//li
```

**substring()**

可以从字符串中，截取指定的内容。

参数;

第一个:开始截取位置的索引(包括开始位置)-

第二个:结束位置的索引（不包括结束位置)

不同的是**substring()**不接受负值，默认将负值转为0

它还会自动调整参数的位置，如果第二个参数小于第一个，则自动交换

**substr()**

用来截取字符串参数:

1.截取开始位置的索引

**2.截取的长度**

**split()**

将一个字符串拆分中一个数组

参数;需要一个字符串作为参数，将会根据该字符串去拆分数组

```
var str = "liuqiang,love,yuwenzhu"
console.log(str.split(","))//['liuqiang', 'love', 'yuwenzhu']
```

**toUpperCase()、toLowerCase()**

```
var str = "liuqiangloveyuwenzhu"
str1 = str.toUpperCase()
console.log(str1)//LIUQIANGLOVEYUWENZHU
console.log(str1.toLowerCase())//liuqiangloveyuwenzhu

```



## 九、对象集

### Date对象

**创建一个Date对象**

```javascript
var d = new Date()
console.log(d)//Sun Nov 28 2021 15:07:23 GMT+0800 (中国标准时间)
```

**创建一个指定的时间对象**

需要构造函数中传递一个表示时间的字符串作为参数

日期的格式		月/日/年  时:分:秒

```javascript
var d2 = new Date("10/28/1997 11:10:30")
console.log(d2)//Tue Oct 28 1997 11:10:30 GMT+0800 (中国标准时间)
```

**获取当前日期对象是几日**

getDay()表示周几

getDay()表示几月 从0开始 表示1月

getTime() 获取当前日期对象的时间戳

时间戳，指的是从格林威治标准时间的1978年1月1日，0时0分0秒到当前日期所花费的毫秒数（1秒= 1000毫秒）

```javascript
var d = new Date()
var day = d.getDay()
var month = d.getMonth()
var time = d.getTime()
console.log(day)// 0 表示周日
console.log(month)//10 表示11月
console.log(time) //1638084317260
```

### Math对象

Math和其他的对象不同，它不是一个构造函数

它属于一个**工具类**不用创建对象，它里面封装了数学运算相关的属性和方法。

```javascript
console.log(Math.PI)//3.141592653589793
```

**abs()**

可以用来计算一个数的**绝对值**

```javascript
console.log(Math.abs(-1)) //1
```

**ceil()**

可以对一个数进行**向上取整**，小数位只有有值就自动进1

```javascript
console.log(Math.ceil(1.1)) //2
```

**floor()**

可以对一个数进行**向下取整**，小数位只有有值就自动进1

```javascript
console.log(Math.floor(1.9)) //1
```

**round()**

可以对一个数进行**四舍五入取整**

```javascript
console.log(Math.round(1.4)) //1 
```

**random()**

可以生产0-1之间的随机数

```javascript
//生产0-10的随机数
console.log(Math.round(Math.random()*10))
//生产1-10的随机数
console.log(Math.round(Math.random()*9)+1)
```

**max()和min()**

可以对几个数求最大最小值

**pow(x,y)**

返回x的y次幂

**sqrt()**

返回一个数的平方根

## 十、包装类

JS中为我们提供了三个包装类，通过这三个包装类可以将基本数据类型的数据转换为对象。注意是**对象**.

**String()**

可以将基本数据类型字符串转换为String对象

**Number()**

可以将基本数据类型的数字转换为Number对象

**Boolean()**

可以将基本数据类型的布尔值转换为Boolean对象

```javascript
var num = new Number(3)
var str = new String(”hello")
var bool = new Boolean(true)javascript

//向num中添加一个属性
num.hello = "asd"
```

**方法和属性可以添加给对象。但不饿能添加给基本数据类型**

当我们对一些基本数据类型的值去调用属性和方法时，浏览器**会临时使用包装类将其转换为对象，然后调用对象的属性和方法。**

调用完以后，在将其转换为基本数据类型。

```javascript
var s = 12
s = s.toString()
console.log(typeof s) //string
s.hello = "2"//转换对象一次
console.log(s.hello) //转换对象又一次不是同意一个对象 所以underfnd
```

## 十一、正则表达式

#### **创建正则表达式的对象**

```javascript
//语法
var reg = new RegExp("正则表达式","匹配模式")
匹配模式可以是 
    i 忽略大小写  
    g 全局匹配模式

使用typeof检查正则对象，会返回object
```

**正则表达式的方法**

**test（）**使用这个方法可以检查一个字符串是否负责正则表达式的规则，符合返回true

```javascript
var reg = new RegExp("a")
var str = "a"
reg.test(str)//true

var reg = new RegExp("a","i")
var str = "ASD"
reg.test(str)//true
```

#### 自变量创建正则表达式

```javascript
//语法
var 变量 = /正则表达式/匹配模式
使用字面量的方式创建更加简单
使用构造函数创建更加灵活
```

```javascript
reg = /ab/
console.log(reg.test("abcd"))//true
```

使用|表示或者的意思

```javascript
reg = /a|b|c/
console.log(reg.test("bcd"))//true
```

创建一个正则表达式检查一个字符串中是否含有字母i

. 查找单个字符 除了换行和行结束符  单独的 . 需要转移字符 \.

[]里的内容也是或的关系

[ab] == a|b

[a-z]任意小写字母

[A-Z]任意大写字母

[A-z] 任意字母

```javascript
//检查一个字符串中是否含有abc 或adc 或aec
reg = /abc|adc|aec/
console.log(reg.test("afc")) //false
reg1 = /a[bed]c/
console.log(reg1.test("abc")) //true
//检查一个字符串不是ab
reg1 = /[^ab]/  
console.log(reg1.test("abc")) //true
```

#### 字符串和正则

**split()**

```javascript 
var str = "1asd2asq3we"
//split()可以传递一个正则表达式作为参数，这样方法将会根据正则表达式去拆分字符串
console.log(str.split(/[0-9]/))//['', 'asd', 'asq', 'we'] 不加“”
```

**search()**

可以搜索字符串中是否含有指定内容

如果搜索到指定内容，则会**返回第一次出现的索引**，如果没有搜索到返回-1

它可以接受一个正则表达式作为参数，然后会根据正则表达式去检索字符串

search()只会查找第一个，即使设置全局匹配都没用

```javascript 
var str = "1asd2asq3we"
console.log(str.search("2a"))//4
console.log(str.search(/2[A-z]s/))//4
```

**match()**

可以根据正则表达式，从一个字符串中将符合条件的内容提取出来。

默认只找到第一个符合要求的内容，我们可以设计全局模式匹配所有内容

**可以为一个正则表达式设置多个匹配模式，且顺序无所谓**

match会将匹配的内容封装到数组中返回

```javascript 
var str = "1asS2asq3We"
console.log(str.match(/[A-z]/))//['a', index: 1, input: '1asd2asq3we', groups: undefined]
console.log(str.match(/[A-z]/g))//['a', 's', 'd', 'a', 's', 'q', 'w', 'e']
console.log(str.match(/[a-z]/ig))//['a', 's', 'd', 'a', 's', 'q', 'w', 'e']
```

**replace()**

可以将字符串中指定内容替换为新的内容

默认只替换第一个

```javascript 
var str = asdasd12axc
console.log(str.replace(/a/,6))//6sdasd12axc
console.log(str.replace(/a/g,6))//6sd6sd126xc
```

#### 特殊字符

```javascript 
\w 任意字符 数字、_  			[A-z0-9_]
\W 除了字符 数字、_ 			[^A-z0-9_]	
\d 任意数字					  [0-9]
\D 除了数字					  [^0-9]	
\s 空格
\S 除了空格
\b 单词边界
\B 除了单词边界
```

单词边界表示一个独立的单词

```javascript 
reg = /\bchild\b/
console.log(reg.test("hello children")) //false
console.log(reg.test("hello child ren"))//true
console.log(reg.test("hellochild ren"))//false
```

#### 量词

通过两次可以设置一个内容出现的次数

量词只对前面的一个内容起作用,需要括号

{n}正好出现n次

{1-m} 出现1到m次

```javascript 
var reg = /a{3}/
//aaa
reg = /(ab){3}/
//ababab
reg = /ab{1,3}c/
//abc abbc abbbc

//+表示至少一个 {1，}
reg = /ab+c/ 
//*表示至少0个到多个 {0，}
reg = /ab*c/
//？表示至少0个到1个 {0，1}
reg = /ab?c/
```

检查字符串中是否以a开头

**^表示开头，$表示结尾**

```javascript 
reg = /^a$/  同s使用只能有一个a
```

#### 手机号的正则表达式

手机号的规则：1 3 567123123（11位）

1. 以1开头   1
2. 第二位3-9任意数字  [3-9]
3. 三位以后任意数字9个 [0-9]{9}

```javascript 
var phone = "15755337162"
var reg = /^1[3-9][0-9]{9}$/
console.log(reg.test(phone))
```

#### 邮件的正则表达式

1102644615  @xx .com . cn

任意字母数字下划线 @ 任意字母数字 . 任意字母

```javascript 
var reg = /[A-z0-9]{3,}@[A-z0-9]+(\.[A-z]{2,5}){1,2}/ 
console.log(reg.test("1102644615@qq.com"))//true
```

## 十二、DOM

Dom全称Document Object Model 文档对象模型

JS中通过DOM来对HTML文档进行操作。只要理解了DOM就可以随心所欲的操作WEB页面。

**文档**

文档表示的就是整个的HTML网页文档对象

**对象**

表示将网页中的每一个部分都转换为了一个对象。

**模型**

使用模型来表示对象之间的关系，这样方便我们获取对象。

### 节点

Node --构成HTML文档最基本的单元

常用节点分为四类：

- **文档节点**：整个HTML文档
- **元素节点**：HTML文档中的HTML标签
- **属性节点**：元素的属性
- **文本节点**：HTML标签中的文本内容

![image-20211201104511913](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211201104511913.png)

![image-20211202095213929](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211202095213929.png)

![image-20211202095316734](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211202095316734.png)

![image-20211202102620272](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211202102620272.png)

### 事件

- 事件，就是文档或浏览器窗口中发生的一些特定的交互瞬间。
- JavaScript 与HTML之间的交互是通过事件实现的。
- 对于Web应用来说，有下面这些代表性的事件︰点击某个元素、将鼠标移动至某个元素上方、按下键盘上某个键，等等。

#### 文档的加载

浏览器在加载一个页面时，是按照自相而下执行的。

读取到一行就运行一行，如果将script标签写道页面的上边，代码执行时，页面还未加载。

**所以可以放在body下面或者用onload方法。**

该事件对应的响应函数将会在页面加载完成之后执行，这样可以确保我们的代码执行时所有的DOM对象已经加载完毕了，

```javascript
window.onload = function() {
    var btn = document.getElementById("btn")
    btn.onclick = function() {
        console.log(123)
    }
}
```

### 剩余dom节点查询

在document中有一个属性body，它保存的是body的引用

```javascript
var body = document.body
```

html根标签

```javascript
var html = document.documentElement
```

all underfind 但是可以打印长度，代表页面中所有的元素 需要用数组打印

```javascript
var all = document.all
```

querySelector()可以根据一个css选择器来查询元素对象

querySelectorAll()可以查询多个，不同的是它将会将符合条件的元素封装为一个数组

```javascript
var div = document.querySelector(".box1 div")
var divs= document.querySelectorAll(".box1 div")
```

### dom增删改

#### appendChild(新节点)

添加一个li节点到body中

```javascript
    var li = document.createElement("li")
    var text = document.createTextNode("合肥")
    li.appendChild(text)
    document.getElementsByClassName("city")[0].appendChild(li)
```

#### insertBefore(新节点，旧节点)

```javascript
    var li2 = document.createElement("li")
    var text2 = document.createTextNode("芜湖")
    li2.appendChild(text2)
    document.getElementsByClassName("city")[0].insertBefore(li2,li)
```

#### replaceChild(新节点，旧节点)

同理同上

#### removeChild(旧节点)

以上都是父节点调用，可以自己调用自己

```javascript
li.parentNode.removeChild(li)
```

#### innerHTML

```
    document.getElementsByClassName("city")[0].innerHTML+='<li>滁州</li>'
```

### 其他样式

**clientwidth**

**clientHeight**

这两个属性可以获取元素的可见宽度和高度

这些属性都是不带px的，返回都是一个数字，可以直接进行计算

会获取元素宽度和高度，包括内容区和内边距

这些属性都是只读的，不能修改

**offsetwidth**

**offsetHeight**

获取元素的整个的宽度和高度，包括内容区、内边距和边框

**offsetParent**

可以获取当前元素的定位父元素

会获取到离当前元素**最近开启定位的祖先元素**，如果都没有，返回body

**offsetLeft**

**offsetTop**

当前元素相对于其定位父元素的水平偏移量

当前元素相对于其定位父元素的垂直偏移量

**scrollwidth**

**scrollHeight**

可以获取元素整个滚动区域的高度

**scrollLeft**

可以获取水平滚动条滚动的距离

**scrollTop**

可以获取垂直滚动条滚动的距离 

### 事件对象

当事件的响应函数被触发时，浏览器每次都会将一个**事件对象作为实参**传递进响应函数。

```javascript
arediv.onmousemove = function(event){
    
	var x = event.clientX
        var y = event.clientY
	alert(x,y )
}
```

ie8下 就是window.event

```js
//解决兼容性问题
var event= event || window.event
```

### 时间冒泡 Bubble

所谓的冒泡指的就是事件的向上传导，当后代元素上的事件被触发时，其祖先元素的相同事件也会被触发。 

```html
//点击sapn  会出发三次alert    
<script>
        window.onload = function() {
            var box = document.getElementById("box1")
            box.onclick = function() {
                alert("box")
            }
            var box = document.getElementById("s1")
            box.onclick = function() {
                alert("span")
            }
            document.onclick = function() {
                alert("document")
            }
        }
    </script>

<body>
    <div id="box1">
        我是box
        <span id="s1">我是span</span>
    </div>
</body>
```

**取消冒泡**

//可以将事件对象的cancelBubble设置为true,即可取消冒泡

```js
event.cancelBubble = true
```

设置三次

```js


    <script>
        window.onload = function() {
            var box = document.getElementById("box1")
            box.onclick = function(event) {
                alert("box")
                event.cancelBubble = true
            }
            var box = document.getElementById("s1")
            box.onclick = function(event) {
                alert("span")
                event.cancelBubble = true
            }
            document.onclick = function() {
                alert("document")
            }
        }
    </script>


```

### 事件委派

为每一个超链接都绑定一个单击响应函数。

那我们就给其父元素添加绑定元素。

**由祖先元素过渡到后代元素，利用了冒泡，减少事件绑定次数**

```html
<script>
    window.onload = function() {
        var ul = document.getElementsByClassName("ul")[0]
        ul.onclick = function(event) {
            alert(event.target.className)
        }
    }
</script>

<ul class="ul">
    <li><a href="javascript:;" class="link1">链接</a></li>
    <li><a href="javascript:;" class="link2">链接</a></li>
    <li><a href="javascript:;" class="link3">链接</a></li>

</ul>
```

### 事件的绑定

**addEventListener()**

通过这个方法也可以为元素绑定响应函数,**不会覆盖。onclick会覆盖**

参数：

1. 事件的字符串，不要on
2. 回调函数，当事件触发时该函数会被调用
3. **是否在捕获阶段触发**，布尔值，一半为false
4. 按照绑定顺序一次执行

```js
btn.addEventListener("click",function(){
	alert(1)
},false)

btn.addEventListener("click",function(){
	alert(2)
},false)

btn.addEventListener("click",function(){
	alert(3)
},false)
```

![image-20211210213505326](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211210213505326.png)

![image-20211210213555710](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211210213555710.png)

### 事件传播

关于事件的传播网景公司和微软公司有不同的理解

- 微软公司认为事件应该是由内向外传播，也就是当事件触发时，应该先触发当前元素上的事件，然后再向当前元素的祖先元素上传播，也就说事件应该在冒泡阶段执行。
- 网景公司认为事件应该是由外向内传播的，也就是当前事件触发时，应该先触发当前元素的最外层的祖先元素的事件，然后在向内传播给后代元素

w3C综合了两个公司的方案，将事件传播分成了三个阶段：

1. **捕获阶段**

   在捕获阶段时从最外层的祖先元素，向目标元素进行事件的捕获，但是默认此时不会触发事件

2. **目标阶段**

   事件捕获到目标元素，捕获结束开始在目标元素上出发事件

3. **冒泡阶段**

   事件从目标元素向他的祖先元素传递，依次触发祖先元素上的事件。

![image-20211211111425218](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211211111425218.png)

如果希望在捕获阶段触发事件，可以将addEventListener()第三个参数设置为true,一般情况下我们不会希望在捕获阶段触发事件，所以这个参数一般都是false

### 拖拽

拖拽的流程：

1. 当鼠标在被拖拽元素上按下时，开始拖拽 **onmousedown**
2. 当鼠标移动时被拖拽元素跟随鼠标移动 **onmousemove**
3. 当鼠标松开时，被拖拽元素固定在当前元素 **onmouseup**

需要嵌套

```js
        window.onload = function() {
            var box = document.getElementById("box1")
            box.onmousedown = function() {

                document.onmousemove = function(event) {
                    event = event || window.event
                    var left = event.pageX
                    var top = event.pageY

                    //修改box的位置
                    box.style.left = left + "px"
                    box.style.top = top + "px"

                }
                box.onmouseup = function() {
                    document.onmousemove = null

                }
            }
        }


    <div id="box1">
        我是box
    </div>
```

### 滚轮

 onmousewheel鼠标滚轮滚动的事件，会在滚轮滚动时触发，**但是火狐不支持该属性**

```js
           box.onmousewheel = function() {
                box.style.height = box.style.height + '10px'
            }
```

在火狐中需要使用DOMMouseScroll来绑定滚动事件注意该事件

需要通过addEventListener(()函数来绑定

```js
window.onload = function() {
    var box = document.getElementById("box1")
    box.onmousewheel = function(event) {
        box.style.height = box.clientHeight + 10 + 'px'
        event.preventdefault()
        //event可以获取鼠标滚轮转动的方向
        //向上滚120 向下滚-120
        alert(event.wheelDelta)
        //火狐
        alert(event.detail)
        
    }
}
```

### 键盘事件

**onkeydown**

按键被按下

**onkeyup**

按键被松开

键盘事件一般都会绑定给一些可以获取到焦点的对象或者是document

可以通过keyCode来判断按键的编码

```js
            document.onkeydown = function(event) {
                console.log(event.keyCode)
                if (event.keyCode === 89 && event.ctrlKey) {
                    console.log("y和ctrl都按下了")
                }
            }
```

**让文本框不能输入数字**

```js
        document.onkeydown = function(event) {
            console.log(event.keyCode)
            if (event.keyCode >=48 && event.keyCode <=57) {
                return false
            }
        }
```

## 十三、BOM

- **浏览器对象模型**
- BOM可以是我们通过**JS来操作浏览器**
- 在BOM中为我们提供了一组对象，用来完成**对浏览器的操作**。
- **BOM对象**
  - **window**：代表整个浏览器的窗口，同时winow也是网页中的全局对象
  - **Navigator**：代表当前浏览器的信息，通过该对象可以来识别不同的浏览器
  - **Location**：代表当前浏览器的地址栏
  - **History**：代表浏览器的历史记录，可以通过该对象来操作浏览器的历史记录。由于隐私问题，不能获取具体的历史记录，只能向前向后翻页，只在当前会话有效！
  - **Screen**：代表用户的屏幕信息，通过该对象可以获取到用户的显示器的相关信息
  - 这些对象都是作为window对象的属性保存的，可以通过**window对象来使用，也可以直接使用**

### Navigator判断浏览器

由于历史原因，Navigator对象中的大部分属性都已经不能帮助我们识别浏览器了

一般我们只会使用**userAgent来判断浏览器的信息**，

```js
        console.log(navigator)//Navigator {vendorSub: '', productSub: '20030107', vendor: 'Google Inc.', maxTouchPoints: 0, userActivation: UserActivation, …}
        var user = navigator.userAgent

        console.log(user)//Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.93 Safari/537.36

        if (/Chrome/i.test(user)) {
            alert("谷歌浏览器")
        }else if (/msie/i.test(user)){
            alert("ie浏览器") //ie11中已经去除，ie11以下可以
        }
```

如果不能通过userAgent来判断，可以通过浏览器中**特有的对象**，来判断浏览器的对象。

比如，**ActiveXObject**

```js
if (window.ActiveXObject) {
    alert("你是ie")
} else {
    alert("你不是ie")
}

//上面不管用了 用的太多了
if ("ActiveXObject" in window) {
    alert("你是ie")
} else {
    alert("你不是ie")
}

```

### History

向前向后翻页

![image-20211219161657170](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211219161657170.png)

**length**

属性，获取当前访问的历史链接数量

#### 方法

**back()**

用来回退到上一个页面

**forward()**

用来跳转到下一个页面

**go()**

可以跳转到指定的页面

它需要一个整数作为参数

​	1表示向前跳转一个页面

​	2表示向前跳转一个页面

​	-1表示向后跳转一个页面

​	-2表示向后跳转一个页面

### Location

如果直接打印location，则可以获取到地址栏的信息(当前页面的完整路径)

如果将location属性修改为一个完整的路径，或者相对路径，则我们页面会自动跳转到该路径，并且**会生成相应的历史记录**。

![image-20211220092607485](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211220092607485.png)

**assign()**

用来跳转到其他页面，作用和直接修改location一样

```js
location.assign("2.html")
```

**reload()**

用于重新加载当前页面，刷新

**如果方法中传递一个true作为参数，则会强制清空缓存刷新页面**

```js
location.reload(true)
```

**replace()**

可以使用一个新的页面替换当前页面，调用完毕也会调换页面

不会生产历史记录，不能使用回退按钮回退

```js
location.replace("2.html")
```

## 十四、定时器

### setInterval()

- 定时调用
- 可以将一个函数，每个一段时间执行一次
- 参数：
  1. 回调函数，该函数会没隔一段时间调用一次
  2. 每次调用间隔时间，单位是毫秒
- 返回值：返回一个Number类型的数据，**定时器的唯一标识**

```js
window.onload = function() {
    var count = document.getElementById("h1")
    num = count.innerText
    setInterval(function() {
        count.innerText = num++
    }, 1000)
}
```

### clearInterval()

用来关闭一个定时器，需要定时器的标识作为参数

```js
var count = document.getElementById("h1")
num = count.innerText
var timer = setInterval(function() {
    count.innerText = num++
    //设置条件关闭，不然放在外面直接就关了
   	if(num ==11) clearInterval(timer)
}, 1000)

```

在开启定时器之前，一定要将上一个定时器关闭

### setTimeOut()

延时调用

延时调用一个函数不马上执行，而是隔一段时间以后在执行,**只会执行一次**

```js
setTimeout(function() {
    count2.innerText = 123
}, 3000)
```

### clearTimeOut()

用来关闭一个延时调用器，需要延时调用器的标识作为参数

```js
qivar timer = setTimeout(function() {
    count2.innerText = 123
}, 3000)

clearTimeOut(timer)
```

## 十五、JSON

- JS中的对象只有js可以识别

- json就是一个**特殊结构的字符串**，并可以转换为任意语言中的对象

- json和js对象格式一样，但是json字符串中的**属性名必须加双引号**

- **json分类：**

  ​	**对象{ }**

  ```js
  var obj="'{"name":"liuqiang","age":18}'
  ```

  ​	**数组[]**

  ```js
  var arr = '[1,2,3,"hello"]'
  ```

- **json中允许的值**

  字符串、数值、布尔值、null、对象、数组

### JSON工具类

工具类JSON，可以帮助一个json转为js对象，也可以将js对象转为json

#### JSON.parse()

可以将以JSON字符串转换为js对象

它需要一个JSON字符串作为参数，会将该字符串转换为JS对象

```js
var obj='{"name":"liuqiang","age":18}'
var s = JSON.parse(obj)
{name: 'liuqiang', age: 18}
```

#### JSON.stringify()

可以将一个JS对象转换为JSON字符串

需要一个js对象作为参数，会返回一个JSON字符串

```js
var obj={name: 'liuqiang', age: 18}
var s = JSON.stringify(obj)
{"name":"liuqiang","age":18}'
```

### eval()

这个函数 可以用来执行一段字符串形式的代码，并将执行结果返回。

如果使用eval()执行的字符串中含有{}。它会将{}当作代码块。可以加一个（）

```js
var obj='{"name":"liuqiang","age":18}'
var obj2 = eval("("+obj+")")
console.log(obj2)  //{name: 'liuqiang', age: 18}
```

可以解决ie7识别不了json类的问题

# JavaScript进阶

## 基础总结

### 数据类型分类

**基本(值)类型**

- String：任意字符串
- Number：任意数字
- boolean：true/false
- underfind
- null

**对象(引用)类型**

- Object：任意对象
- Function：一种特别对象（可以执行）
- Array：：一种特别对象（数字下标属性）

### 判断

**typeof()**

返回数据类型的**字符串表达**，即返回字符串

可以判断：underfind/数值/字符串/布尔值

**不能判断：null与Object、Object与array**

```js
var a
console.log(a)	undefined
console.log(typeof a)	'undefined'
console.log(undefined === 'undefined')	false
console.log(typeof a) === 'undefined')	true
console.log(a=== undefined)	true

a = 2
console.log(typeof a)	'number'
a = '123'
console.log(typeof a)	'string'
a = true
console.log(typeof a)	'boolean'
a = null
console.log(typeof a)	'object'
```

**instanceof()**

专门用来**判断对象**的类型

判断是不是它的实例 

```js
var b1 = {
b2: [1, 'abc'],
b3: function() {

}
}
console.log(b1 instanceof Object, b1 instanceof Array)	true false
console.log(b1.b2 instanceof Array, b1.b2 instanceof Object)	true true
console.log(b1.b3 instanceof Function, b1.b3 instanceof Object)	true true
console.log(typeof b1.b3 === 'function') true
```

### 用法

#### 什么时候赋值null

**初始赋值，表明将要赋值的对象**

```js
var obj = null
```

**结束，让对象称为垃圾对象，被垃圾回收器回收**

```js
var obj = 123
obj = null
```

#### 变量类型和数据类型

**变量类型(变量内存值的类型)**

- 基本类型：保存的是基本类型的数据
- 引用类型：保存的是地址值

**数据类型**  

- 基本类型
- 对象类型

#### 内存、数据、变量三者之间的关系

- **内存是用来存储数据的空间**

- 变量是可变化的量，由变量名和变量值组成。

  每个变量都对应着一块内存，变量名用来查找对应的内存，变量值保存内存中的数据。

  **变量是内存的标识。**

#### 引用变量赋值

2个引用变量指向用一个对象，通过一个变量修改对象内部数据，另一个变量看到的是**修改后的数据**。

```js
var obj1 = {name:'Tom'}
var obj2 = obj1
obj2.age = 18
console.log(obj1.age) 18
function fn (obj){
	obj.name = 'A'
}
fn(obj1)
console.log(obj2.name)  A
```

2个引用变量指向同一个对象 ，让其中一个引用变量指向另一个对象，另一引用变量依然指向前一个对象

```js
var a ={age:12}
var b = a
a = {name:'Bob',age:13}
console.log(b.age,a.name,a.age)  12   Bob 13

注意看！！
function fn2(obj){
    obj = {name:'asd'}
}

fn2(a)
console.log(a.name) 'Bob' 容易犯错，函数里面的对象已经被垃圾函数回收了
```

#### 值传递

js调用函数时传递变量参数，都是**值传递！！！！**

一个传的值基本数据，一个传的是这个对象的地址

```js
var a =3
function fn(a){
	a = a+1
}
fn(a)
console.log(a) 3


function fn2(obj){
    console.log(obj.name)
}

var obj ={name:'liuqiang'}
fn2(obj)
```

读取实参值。赋值给形参

#### JS引擎管理内存

#### 内存生命周期

1. 分配小内存空间，得到他们的使用权
2. 存储数据，可以反复进行操作
3. 释放小的内存空间

#### 释放内存

**局部变量**：函数执行完自动释放

**对象**：称为垃圾对象==》垃圾回收税收

## 二、函数高级

### 1.原型与原型链

#### prototype

 **函数的prototype属性**

- 每个函数都有一个prototype属性，它默认指向一个Object空对象(即称为：原型对象)，Object函数不满足。

  ```js
  Fn.prototype instanceof Object    //true
  Object.prototype instanceof Object //false
  Function.prototype instanceof Object //true
  ```

- 原型对象重有一个属性constructor，它执行函数对象

- 只有函数有。实例对象没有

**给原型对象添加属性**

- 作用：函数的所有实例对象自动拥有原型中的属性或者方法
- 原型上的方法是给实例对象使用的

```js
console.log(Date.prototype)	{constructor: ƒ, toString: ƒ, toDateString: ƒ, toTimeString: ƒ, toISOString: ƒ, …}
console.log(typeof Date.prototype) 	'object'


function fn(){}
//给原型对象添加属性
fn.prototype.test =function(){}

console.log(fn.prototype)	{test: ƒ, constructor: ƒ}
console.log(fn.prototype.constructor == fn) 	true

var obj = new fn()
obj.test()
```

#### 显式原型和隐式原型

- 每个函数function都有一个prototype,即**显式原型**

  ```js
  var fn =function(){}
  console.log(fn.prototype)	constructor: ƒ}
  ```

- 每个实例对象都有一个\_proto\_,可称为**隐式原型**

  ```js
  var f = new fn()
  console.log(f.__proto__)	{constructor: ƒ}
  ```

- 对象的隐式原型的值就是它对构造函数的显式原型的值                                            

  对象.\_proto\_=对象的构造函数.prototype

  ```js
  fn.prototype ===f.__proto__ 	true
  ```

- 总结：

  函数的prototype属性:	在定义函数时自动添加的，默认值是一个空object对象	

  对象的_proto\_属性:	创建对象时自动添加的，默认值为构造函数的prototype属性值

  程序员能直接操作显式原型，但不能直接操作隐式原型(ES6之前)

  ```js
  fn.prototype.test = function(){
      console.log('test')
  }
  f.test()	test
  ```

  

#### 原型链

访问一个对象的属性时，

- 先在自身属性重查找，找到返回。
- 如果没有，再沿着\__proto\__这条链上向上查找，找到返回
- 如果最终没找到，返回underfined

别名：**隐式原型链**

最先的方法都是定义在Object函数的原型对象上的

![image-20211223153435564](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211223153435564.png)

所有函数的\__proto\__都是一样的



#### 重点

1. **函数的显示原型指向的对象默认是空object实例对象(但object不满足)**

   ```js
   Fn.prototype instanceof Object    //true
   Object.prototype instanceof Object //false
   Function.prototype instanceof Object //true
   ```

2. **所有函数都是Function的实例（包括Function本身）**

   最特殊的是。**Function的\__proto\__和prototype是一样的**，都指向Function的原型对象

   ```js
   Function.__proto__ == Function.prototype
   ƒ () { [native code] }
   ```

   **Function函数的constructor指向的是它自己本身，**

   ```js
   Function.constructor == Function
   ```

   **Function的原型对象的constructor指向Function函数**

   ```js
   Function.prototype.constructor == Function //true
   ```

3. **Object的原型对象是原型链的尽头**

   ```js
   Object.prototype.__proto__  //null
   ```

![image-20211223165800155](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211223165800155.png)

#### 原型的属性

**读取对象的属性值时**：自身没有的话，会自动到原型链中查找

**设置对象的属性时**：不会查找原型链，如果当前对象中没有此属性，直接添加此属性并设置其值。

**方法一般定义在原型中，属性一般通过构造函数定义在对象本身上。**

```js
function fn(){}

fn.prototype.a = 123

var f1= new fn()

console.log(f1.a)  //123

var f2 = new fn()
f2.a =456

console.log(f1.a) //123
console.log(f2.a)//456
```

属性在对象中，方法在原型对象中

```js
function Person(name,age){
	this.name = name
	this.age = age
}
Person.prototype.setName = function(name){
	this.name = name
}

var p = new Person("刘强",18)
p.setName('yuwenzhu')
console.log(p)
```

![image-20211223194721503](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211223194721503.png)

#### instanceof

A instanceof B

如果B函数的显式原型对象在**A对象的原型链上**，返回true，否则返回false

Function是通过new自己产生的实例

![image-20211223195839794](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211223195839794.png)

案例1

```js
function Foo(){}
var f1 = new Foo()
console.log(f1 instanceof Foo) //true
console.log(f1 instanceof Object) //true
```

案例2

```js
console.log(Object instanceof Function)//true
console.log(Object instanceof Object)//true
console.log(Function instanceof Function) //true
console.log(Function instanceof Object)//true

//不能逆序 
function Foo(){}
console.log(Function instanceof Foo)//tfalse
```

### 2.执行上下文

**代码分类**分为全局代码、函数代码变量提升和函数提升

 **变量提升**

通过var定义声明变量时，在定义语句之前就可以访问到。值为underfined

**函数声明提升**，不是函数表达式

通过**function声明**的函数，在之前就可以直接调用，值：函数定义(对象)

```js
var a =3
function fn(){
       //相当于 var  a；
	console.log(a)
	var a =4
}
fn() 输出underfined，

console.log(b)  underfined 变量提升 
var b=3

fn2()  可提前调用 函数声明提升
function fn2(){
    consooe.log('f2')
}

fn3() 报错 因为fn3变量提升只是一个undefined，不饿能调用
var fn3 = function (){
    consooe.log('f3')
}


```

**先执行变量提升，再执行函数提升**

```js
function a(){}
var a;
console.log(typeof a)	 function
所有先a变量声明，再函数声明了
```

**条件语句的var也算进去**

```js
if (!(b in window)){
	var b =1
}
console.log(b) underfined
因为变量提升了 所有b有了 所有条件不成立
```

再想想！！！

```js
var c =1
function c(c){
    console.log(c)
}
c(2) 
可以换算成 


var c;
function c(c){
    console.log(c)
}
c = 1 //这个时候c已经是函数了 然后赋值成1 
c(2)  //numer类型了 不是函数了报错

```

#### 全局执行上下文

执行顺序如下：

1. 在执行全局代码前将window确定为window属性
2. 对全局数据进行预处理
   - var 定义的全局变量==》underfined，添加为window属性
   - function声明的全局变量==》赋值(fun)，添加为window的方法
   - this==>赋值(window)
3. 开始执行全局代码

#### 函数执行上下文

**调用函数才会创建函数执行上下文**

执行顺序如下：

1. 在调用函数，准备执行函数体之前，创建对应的函数的执行上下文
2. 对局部数据进行预处理
   - 形参变量==》赋值(实参)==》添加为执行上下文的属性
   - arguments==》赋值(实参列表)==》添加为执行上下文的属性
   - var定义的局部变量==》underfined，添加为执行上下文的属性
   - function声明的全局变量==》赋值(fun)，添加为执行上下文的属性
   - this==>赋值(调用函数的对象)
3. 开始执行函数体代码



```js
全局执行上下文
console.log(a1, window.a1) //undefined
console.log(a2, window.a2)
// ƒ a2() {
//     console.log(2)
// }

console.log(this) //Window {window: Window, self: Window, document: document, name: '', location: Location, …}

var a1 = 3

function a2() {
    console.log(2)
}

函数执行上下文
function fn(a1) {
    console.log(a1) //2
    console.log(a2) //underined
    a3() //fun()

    console.log(this) ///Window {window: Window, self: Window, document: document, name: '', location: Location, …}
    console.log(arguments) //Arguments(2) [2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]

    var a2 = 3

    function a3() {
        console.log('fun()')
    }
}
```

#### 执行上下文栈

1. 在全局代码执行前，JS引擎就会**创建一个栈**来存储管理所有的执行上下文对象
2. 在全局执行上下文（window）确定后，将其添加到栈中（压栈）
3. 在函数执行上下文创建后，将其其添加到栈中（压栈）
4. 在当前函数执行完后，将栈顶的对象溢出（出栈）
5. 当所有的代码执行完后，**栈中只剩下window**

### 3.作用域与作用域链

**理解**

就是一块地盘，一段代码所在的区域

它是静态的，相对于上下文对象，再编写代码时就确定了

**分类**

全局作用域

函数作用域

没有块作用域（ES6有了）

**作用**

隔离变量，不同作用域下同名变量不会冲突

```js
var a = 10,b =20
function fn(x){
    var a = 100,c=300
    console.log('fn',a,b,c,x)
    function bar (x){
        var a =1000,d=400
        console.log('bar()',a,,b,c,d,x)
    }

    bar(100)
    bar(200)
}
fn(10)

fn 100 20 300 10
bar() 1000 20 300 400 100
000 20 300 400 200
```

#### 作用域和执行上下文的区别

**区别1**

1. 全局作用域之外，每个函数都会创建自己的作用域，**作用域在函数定义时就已经确定了**，而不是函数调用时。
2. 全局执行上下文环境是在全局作用域确定之后，js代码马上执行之前创建。
3. 函数执行上下文是在调用函数时，函数体代码执行之前创建的

**区别2**

1. 作用域是**静态**的，只要函数定义好了就一直存在，不会变化
2. 上下文环境是**动态**的，调用函数时创建，函数调用结束时上下文环境就会自动被释放

**联系**

上下文环境（对象）是**从属于**所在的作用域

全局上下文环境==》全局作用域

函数上下文环境==》对应的函数作用域





**面试练习**

```js
var x = 10

function fn() {
    console.log(x)
}

function show(f) {
    var x = 20
    f()
}
show(fn)
```

结果是10，fn作用域找x,可是没有只能去全局去找！

作用域已经在函数定义时就有了固定死了

![image-20211231162752954](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211231162752954.png)





```js
var f1 = function() {
    console.log(f1)
}
f1()
var obj = {
    f2: function() {
        console.log(f2)
    }
}
obj.f2()


var obj 2= {
    f3 :function() {
        console.log(this.f3)
    }
}
obj2.f3()
```

输出结果,fn2去全局作用域去找

```js
ƒ () {
    console.log(f1)
}
Uncaught ReferenceError: f2 is not defined
at Object.f2 (4.html:30)
at 4.html:33

ƒ () {
            console.log(this.f3)
        }

```

### 4.闭包

#### 循环遍历的变量问题

```js
window.onload = function() {
    var buttons = document.getElementsByTagName('button')

    for (var = 1; i <= buttons.length; i++) {
        var obj = buttons[i - 1]
        obj.onclick = function() {
            console.log('这是按钮' + i)
        }
    }
}

<body>
    <button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>
</body>
```

点击按钮都是4，为什么呢？

**可以这样解决**

```js
解决方案1：块声明
window.onload = function() {
    var buttons = document.getElementsByTagName('button')
    for (let i = 1; i <= buttons.length; i++) {
        var obj = buttons[i - 1]
        obj.onclick = function() {
            console.log('这是按钮' + i)
        }
    }
}


解决方案 2： 对象变量
window.onload = function() {
    var buttons = document.getElementsByTagName('button')

    for (var i = 1; i <= buttons.length; i++) {
        var obj = buttons[i - 1]
        obj.index = i
        obj.onclick = function() {
            console.log('这是按钮' + this.index)
        }
    }
}

解决方案 3： 闭包解决
    window.onload = function() {
        var buttons = document.getElementsByTagName('button')

        for (var i = 1; i <= buttons.length; i++) {
            (function(i) {
                var obj = buttons[i - 1]
                obj.onclick = function() {
                    console.log('这是按钮' + i)
                }
            })(i)
        }
    }
```

#### 闭包定义

当一个嵌套的内部函数引用了嵌套外部函数的变量时，就产生了闭包。

就是**内部函数引用了外部函数的数据**

闭包存在于嵌套的内部函数中

```js
function fn(){
    var a = 2
    function fn2(){
        console.log(2)
    }
    fn2()
}
fn()
```

#### 常见的闭包

闭包的特点：函数内部的变量会一直存在于内存中，不会立即释放

##### 将函数作为另一个函数的返回值

```js
window.onload = function() {
    function fn1() {
        var a = 2

        function fn2() {
            a++
            console.log(a)
        }
        return fn2
    }
    var f = fn1()
    f() // 3
    f() // 4
}
```

##### 将函数作为实参传递给另一个函数调用

```js
function showDetail(msg, time) {
    setInterval(() => {
        alert(msg)
    }, time);
}

showDetail("dayin", 1000)
```

#### 闭包的作用

1. 使用函数内部的变量在函数执行完后，仍然存活在内存中（延长了局部变量的声明周期）
2. 让函数外部可以操作(读写)到函数内部的数据（变量/函数）

#### 闭包的生命周期

**产生**：在嵌套内部函数定义执行完时就产生了（不是在调用）

**死亡**：在嵌套的内部函数称为垃圾对象时

```js
function fn1() {
    //闭包已经产生，函数提升，内部函数对象已经创建
    var a = 2

    function fn2() {
        a++
        console.log(a)
    }
    return fn2
}
var f = fn1()
f() // 3
f() // 4
f=null//闭包死亡
```

#### 闭包的应用：定义Js模块

-  具有特别功能的js文件
- 将所有的数据和功能都封装在一个函数内部（私有的）
- 只向外暴露一个包含n个方法的对象
- 模块的使用者 ，只需要通过模块暴露的对象调用方法来实现对应的功能

**myModule.js**

```js
function myModule() {
    //私有数据
    var name = '刘强'
    //操作数据的函数
    function doCoding() {
        console.log(name + "正在doCoding")
    }

    function doSleeping() {
        console.log(name + "正在doSleeping")
    }
    //向外暴露对象使用方法
    return {
        doCoding: doCoding,
        doSleeping: doSleeping
    }
}
```

```js
<script type="text/javascript" src="mymodule.js"></script>    

var fn = myModule()
fn.doCoding()
fn.doSleeping()
```

**使用匿名函数的方式**

myModule.js

```js
(function myModule() {
    //私有数据
    var name = '刘强'
    //操作数据的函数
    function doCoding() {
        console.log(name + "正在doCoding")
    }

    function doSleeping() {
        console.log(name + "正在doSleeping")
    }
    //向外暴露对象使用方法
    window.myModule2={
        doCoding: doCoding,
        doSleeping: doSleeping
    }
})()
```

```js
<script type="text/javascript" src="mymodule.js"></script>    

myModule2.doCoding()
myModule2.doSleeping()
```

可以代码压缩！

#### 闭包的缺点

1. 函数执行完后，函数内的局部变量没有释放，**占用内存时间会变长**
2. 容易造成**内存泄露**（内存白白占用，不使用）

**一定要及时释放！！**

#### 内存溢出与内存泄露

##### 内存溢出

一种程序运行出现的错误，当程序运行需要的内存超过了剩余的内存时，就抛出内存溢出的错误。

```js
var obj = {}

for(let i=0;i<999999;i++){
    obj[i] = new Array[9999999]
}
```



##### 内存泄露

1. 占用的内存没有及时释放
2. 内存泄漏积累多了就很容易导致内存溢出
3. 常见的内存泄露:
   - **意外的全局变量**
   - **没有及时清理的计时器或回调函数**
   - **闭包**

### 面试题

输出什么

```js
var name = 'windows'
var object = {
    name: 'my object',
    getNameFunc: function() {
        var name =123
        return function() {
            var name=456
            return this.name
        }
    }
}
alert(object.getNameFunc()())
```

```js
var name2 = 'windows2'
var object2 = {
    name2: 'my object2',
    getNameFunc: function() {
        var that = this
        return function() {
            return that.name2
        }
    }
}

alert(object2.getNameFunc()())
```

前者输出window 后面输出my object2

**究极问题**

```js
function fun(n, o) {
    console.log(o)
    return {
        fun: function(m) {
            return fun(m, n)
        }
    }
}
var a = fun(0)
a.fun(1)
a.fun(2)
a.fun(3)


```

答案![image-20220103131103194](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220103131103194.png)

![image-20220103131051138](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220103131051138.png)

![image-20220103131039286](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220103131039286.png)

## 三、面向对象高级

### 1.对象创建模式

**方法一：Object构造函数模式**

套路：先创建空对象，再动态添加属性和方法

使用场景：**起始时不确定对象内部数据**

问题：**语句太多**

```js
var p = new Object()
p.name = '刘强'
p.setName = function(name) {
    this.name = name
    console.log(this.name)
}
p.setName("yuwenzhu")
```

**方法二：对象字面量模式**

套路:使用创建对象,同时指定属性/方法

适用场景:起始时对象内部数据是确定的

问题:**如果创建多个对象，有重复代码**

```js
var p = {
    name: '刘强',
    setName: function(name) {
        this.name = name
        console.log(this.name)
    }
}
```

**方法三：工厂模式**

套路:通过工厂函数动态创建对象并返回

适用场景:需要创建多个对象

问题:**对象没有一个具体的类型，都是object类型**

```js
function createPerson(name) {
    var obj = {
        name: name,
        setName: function(name) {
            this.name = name
            console.log(this.name)
        }
    }
    return obj
}

var p1 = createPerson("刘强")
var p2 = createPerson("俞文竹")
console.log(p1.name)
```

**方法四：自定义构造函数模式**

套路: 自定义构造函数，通过new创建对象

适用场景:需要创建多个对象

问题:**每个对象都有相同的数据，浪费内存**

```js
function Student(name) {
    this.name = name
    this.setName = function(name) {
        this.name = name
        console.log(this.name)
    }
}

var o1 = new Person("刘强")
var o2 = new Person("刘强")
console.log(o1, o2)
var p4 = new Person("俞文竹")
```

每个实例对象都有1方法，这种方法建议放在原型对象中

![image-20220103150956257](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220103150956257.png)

```js
function Student(name) {
    this.name = name
}

Student.prototype.setName = function(name) {
    this.name = name
    console.log(this.name)
}
var o1 = new Person("刘强")
```

### 2.继承模式

#### 原型链继承

这是父函数和子函数

```js
//父类型
function Supper() {
    this.supProp = 'Sup'
}

Supper.prototype.showSupperPro = function() {
    console.log(this.supProp)
}

//子类型
function Sub() {
    this.subProp = 'Sub'
}
Sub.prototype.showSubPro = function() {
    console.log(this.subProp)
}

```

实例对象，调用方法会报错.因为sub没这个方法 原型链上也没有

```js
var sub = new Sub()
sub.showSubPro() //Sub
sub.showSupperPro() //报错showSupperPro不是一个fcuntion
```

想要用原型链继承，关键就是子类型的原型对象指向父类的实例对象

```js
var sub = new Sub()
sub.__proto__ = new Supper()
或者
Sub.prototype = new Supper()
sub.showSupperPro() 
```

案例图

![image-20220104121440482](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220104121440482.png)

#### 借用构造函数继承

只是简化代码而已，不算继承

```js
function Person(name, age) {
    this.name = name
    this.age = name
}

function Student(name, age, price) {
    Person.call(this, name, age) //相当于 this.Person(name,age)
    this.price = price
}

var s = new Student('liuqiang', 23, 495)
console.log(s)//Student {name: 'liuqiang', age: 'liuqiang', price: 495}
```

#### 组合继承

```js
function Person(name, age) {
    this.name = name
    this.age = name
}

Person.prototype.setName = function(name) {
    this.name = name
}


function Student(name, age, price) {
    Person.call(this, name, age) //为了得到属性
    this.price = price
}

Student.prototype = new Person() //为了能看到父类型方法
Student.prototype.constructor = Student //为了修正constructor属性
Student.prototype.setPrice = function(price) {
    this.price = price
}
var s = new Student('liuqiang', 23, 495)
s.setName("yuwenzhu")
s.setPrice(666)
console.log(s)
```

![image-20220104124129869](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220104124129869.png)

## 四、线程机制和事件机制

### 1.进程和线程

**进程**

- 程序的一次执行，它占有一片独立的内存空间
- 可以通过windows任务管理器查看进程

**线程**

- 是进程内的一个独立执行单元
- 是程序执行的一个完整流程
- 是CPU的最小的调度单元

![image-20220104151342885](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220104151342885.png)

**要点**

- 应用程序必须运行在某个进程的某个线程上
- 一个进程中至少有一个运行的线程：主线程，进程启动后自动创建
- 一个进程中也可以同时运行多个线程，我们会说程序是多线程运行的
- 一个进程内的数据可以供其中多个线程直接共享
- 多个进程之间的数据时不能直接共享的
- **线程池**：保存**多个线程对象**的容器，实现线程对象的反复利用

#### 问题

##### 何为多进程与多线程？

**多进程**：一应用程序可以同时启动多个实例运行

**多线程**：在一个进程内，同时有多个线程运行

##### 比较单线程与多线程？

**单线程：**

优点：顺序变成简单易懂

缺点：效率低

**多线程**：

​	优点：

1. 能有效提升CPU的利用率

缺点

1. 创建多线程开销
2. 线程间切换开销（来回切换）
3. 死锁与状态同步问题

##### Js是单线程还是多线程？

js是单线程运行的

但使用H5的Web Workers可以多线程运行 

##### 浏览器运行时单线程还是多线程？

**都是多线程运行**

##### 浏览器运行时单进程还是多进程？

有的是单进程：firefox/老ie

有的是多进程：谷歌/新ie

### 2.浏览器内核

![image-20220104160235198](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220104160235198.png)

### 3.定时器思考

#### 保证真正定时执行

定时器并**不能保证真正定时执行** ，一般会延迟一点，也可能延迟很长时间。

```js
var start = Date.now()
console.log("before")
setTimeout(function() {
    console.log("starting:", Date.now() - start)
}, 100)
console.log("after")
//每次刷新页面打印的时间不一样 
```

#### js单线程

定时器的**回调函数是在主线程执行的**，js是单线程的

##### 案例1

```js
setTimeout(function() {
    console.log("2000")
}, 2000)
setTimeout(function() {
    console.log("1000")
}, 1000)

function fn() {
    console.log('fn()')
}
fn()
```

输出 fn 1000 2000

##### 案例2

```js
setTimeout(function() {
    console.log("2000")
}, 2000)
setTimeout(function() {
    console.log("1000")
}, 1000)

function fn() {
    console.log('fn()')
}
fn()

console.log("before")
alert("-------")
console.log("after")
```

alert会展厅主线程的执行，同时暂停计时，点击确定后，恢复一切。

不过现在谷歌不展暂停了！！

##### 案例3

```js
setTimeout(function() {
    console.log("2000")
}, 2000)
setTimeout(function() {
    console.log("1000")
}, 1000)

function fn() {
    console.log('fn()')
}
fn()

console.log("before")
alert("-------")
console.log("after")
```

先输出before ----after 后面是定时器

**Js的引擎执行代码的基本流程**：

1. 先执行初始化代码：包含一些特别的代码
   - 设置定时器
   - 绑定监听
   - 发送ajax
2. 后面再某个时刻执行回调函数

**先执行同步代码，后执行异步代码**

### 4.事件循环模型

**所有代码分类**

**初始化执行代码（同步代码**）：包含绑定dom事件监听，设置定时器，发送ajax

**回调执行代码（异步代码）**：处理回调函数

**js引擎执行代码的基本流程:**

初始化代码===>回调代码

模型的2个重要组成部分：

- 事件管理模块
- 回调队列

模型的**运转流程**：

- 执行初始化代码，将事件回调函数交给对应模块管理
- 当事件发生时，管理模块会将回调函数及其数据添加到回调函数中
- 只有当初始化代码执行完成后，才会遍历读取队列中的回调函数执行

### 5.Web Workers多线程

H5规范了**js分线程**的实现，取名为web workers

相关api

- **Worker**：构造函数，记载分线程执行的js文件
- **Worker.prototype.onmessage**:用于接收另一个线程的回调函数
- **Worker.prototype.postMessage**：向另一个线程发送消息

不足

- Worker内代码不能操作Dom(更新UI)
- 不能跨域加载js
- 不是每个浏览器都能支持这个特性 



**斐波那契数列**

```js
function fibo(num) {
    if (num <= 2) return 1

    return fibo(num - 2) + fibo(num - 1)
}
alert(fibo(3))
```

一旦递归很多的时候，它会一直加载计算，alert页面是动不了的。

所以我们可以将**大计算量的代码交由web Worker运行**而不冻结用户界面

但是子线程完全受主线程控制，且不得操作DOM。

所以这个新标准**并没有改变javascripy单线程的本质**

案例使用如下：

1. 创建在分线程执行的js文件

   ```js
   function fibo(num) {
       if (num <= 2) return 1
   
       return fibo(num - 2) + fibo(num - 1)
   }
   
   var onmessage = function(event) {
       var number = event.data
       console.log('分线程接收到主线程发送的数据：', number)
       var result = fibo(number)
       postMessage(result)
       console.log('分线程向到主线程返回的数据：', result)
   
   }
   console.log(this)
   
   ```

   ![image-20220104204339919](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220104204339919.png)

2. 在主线程中的js中发消息并设置回调

   ```js
   document.getElementById("btn").onclick = function() {
       var num = document.getElementById("in").value
   
       //创建一个Worker对象
       var worker = new Worker('worker.js')
   
       //接收worker传过来的数据函数
       worker.onmessage = function(event) {
           console.log('主线程接收分线程返回的数据：', event.data)
           console.log(event.data)
       }
   
       //向分线程发送消息
       worker.postMessage(num)
       console.log('主线程向分线程发送的数据：', num)
   }
   ```

3. ```js
   主线程向分线程发送的数据： 12
   分线程接收到主线程发送的数据： 12
   分线程向到主线程返回的数据： 144
   线程接收分线程返回的数据： 144
   ```

   

在worker.js 不能调用alert,因为alert是window的方法，在分线程中不可使用。

worker的全局对象不再是window，所以分线程不可能更新界面

![image-20220104204132890](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220104204132890.png)
