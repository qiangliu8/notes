# typescript教程

[TOC]



## 一、快速入门

### 1. TypeScript 简介

1. TypeScript是JavaScript的超集。
2. 它对JS进行了扩展，向JS中引入了类型的概念，并添加了许多新的特性。
3. TS代码需要通过编译器编译为JS，然后再交由JS解析器执行。
4. TS完全兼容JS，换言之，任何的tS代码都可以直接当成JS使用。
5. 相较于JS而言，TS拥有了静态类型，更加严格的语法，更强大的功能；TS可以在代码执行前就完成代码的检查，减小了运行时异常的出现的几率；TS代码可以编译为任意版本的JS代码，可有效解决不同JS运行环境的兼容问题；同样的功能，TS的代码量要大于JS，但由于TS的代码结构更加清晰，变量类型更加明确，在后期代码的维护中TS却远远胜于JS。

![1646482527255](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646482527255.png)

![1646482620245](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646482620245.png)

### 2. TypeScript 开发环境搭建

1. 下载并安装Node.js
   
3. 使用npm全局安装typescript
   - 进入命令行
   - 输入：npm i -g typescript
   
4. 创建一个ts文件

5. 使用tsc对ts文件进行编译
   - 进入命令行
   
   - 进入ts文件所在目录
   
   - 执行命令：tsc xxx.ts

### 3. 基本类型

注意声明都是小写 number，string，boolean

**类型声明**

- 类型声明式TS非常重要的一点
- 通过类型声明可以指定ts中的变量(参数、形参)的类型
- 指定类型后。当为变量赋值时，ts编译器会**自动检查值是否符合类型声明**，符合则赋值，否则报错
- 简而言之，类型声明给变量设置了类型，那么变量只能存储某个类型的值
- 类型：

![1646486359371](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646486359371.png)

ts及时编译有问题，但是还是会进行编译！

**自动类型判断**

- TS拥有自动类型判断机制
- **当变量的声明和赋值是同时进行的，ts编译器会自动判断变量的类型**
- 所以如果你的变量的声明和赋值同时进行的，可以省略掉类型声明。

```ts
//js中函数是不考虑参数的类型和个数的
function fun(a,b){
    return a+b
}
console.log(fun(1,2)) //3
console.log(fun(1,"2"))//12

//ts语法
function fun1(a:number,b:number){
    return a+b
}
console.log(fun1(1,2))//3
console.log(fun1(1,'2'))//ts编译会报错

//要求返回值也是number
function fun2(a:number,b:number):number{
    return a+'hell' //返回是字符串但是要求是number所以编译报错
}

```

**类型**

|  类型   |       例子        |              描述              |
| :-----: | :---------------: | :----------------------------: |
| number  |    1, -33, 2.5    |            任意数字            |
| string  | 'hi', "hi", `hi`  |           任意字符串           |
| boolean |    true、false    |       布尔值true或false        |
| 字面量  |      其本身       |  限制变量的值就是该字面量的值  |
|   any   |         *         |            任意类型            |
| unknown |         *         |         类型安全的any          |
|  void   | 空值（undefined） |     没有值（或undefined）      |
|  never  |      没有值       |          不能是任何值          |
| object  |  {name:'孙悟空'}  |          任意的JS对象          |
|  array  |      [1,2,3]      |           任意JS数组           |
|  tuple  |       [4,5]       | 元素，TS新增类型，固定长度数组 |
|  enum   |    enum{A, B}     |       枚举，TS中新增类型       |
**字面量**

```ts
//可以直接使用字面量进行类型声明
let a:10
a=10
//a=12    报错，不能将类型“12”分配给类型“10”。
//可以使用 |来连接多个类型（联合类型）
let c:'liu'|"yu"
c="liu"
c ="yu"

let d :boolean|string
d=true
d='22'
```
**any任意类型 任意赋值 相当于关闭了ts的类型检测**

```ts
let e:any
e=10
e="2"
e=false
//如果声明变量不指定类型，则ts解析器会自动判断变量的类型为any
let f 
f=12
f='22'
```
**unknown任意类型 任意赋值**  

```ts
let g:unknown
g=10
g='222'
let s:string
s=f //any可以赋值给任何变量 
s=g //unkown就不可以 报错不能赋值给所有变量 只能自己给自己赋值 
```
**类型断言**

```ts
 //告诉解析器变量的实际类型 unkonwn变为string
s= g as string
s = <string>g
```
**void**

```ts
//void用来表示空，以函数为例，就表示没有返回值的函数
function fun3():void{
	return null | undefined
}
```
**nerver 表示永远不会返回结果**

```ts
function fn():never{
    throw 'error'
}
```
**对象object**

```ts
//{}用来指定对象中包括哪些属性
//语法：{属性名：属性值,属性名?(可选)：属性值}
let b:{name:string,age?:number}

b={name:'刘强',age:18}
b={name:'刘强'}

//设置对象
let c:{name:string,[prop:string]:any}
c={name:'刘强',age:18,age1:18,age2:18,age3:'asd'}
//设置函数
let d:(a:numerb,b:number)=>number
d= function(n1,n2):number{
    return n1+n2
}
```
**数组 array 两种表示方式**

```ts
//string[] 表示字符串数组
let e:string[]
e=['a','b','c']
let f:Array[number] //等同并于 f=number[]
f=[1,2,3]
```
**元组 tuple 固定长度的数组 想写几个写几个**

```ts
let h:[string,number]
h=['ws',123]
```
**枚举**

```ts
enum Gender{
    Male=0,
    Female=1
}
let i :{name:string,gender:Gender}
i={
    name:'孙悟空',
    gender:Gender.Male
}
console.log(i.gender==Gender.Male)
```
**&**

```ts
&表示同时
let j:{name:string}&{age:number}
j={name:'刘强',age:23}
```

**类型的别名**

```ts
type myType=1|2|3|4|5
let k :myType
k=1
k=2
```

### 4. 编译选项

**自动编译单个文件**

编译文件时，使用-w指令后，ts编译器会自动监视文件的变化，并再文件发生变化时对文件进行重新编译。

```ts
tsc xxx.ts -w
```

**自动编译整个项目**

1. 先在项目根目录下创建一个ts的配置文件 tsconfig.json

   **tsconfig.json是一个JSON文件，添加配置文件后，只需只需 tsc 命令即可完成对整个项目的编译**

2. 直接使用tsc指令，则可以自动将当前项目下的所有ts文件编译为js文件。

```js
{
    //tsconfig.json是ts编译器的配置文件，ts编译器可以根据它的信息来对代码进行编译
    
    编译常用设置
    //指定哪些文件需要被编译
    //**表示任意目录 *表示任意文件
    "include": [
        "./src/*"
    ],
    //指定哪些文件不需要被编译
    //默认值：["node_modules", "bower_components", "jspm_packages"]
     "exclude": [
         "./src/1.ts"
    ],
    //定义被继承的配置文件 
    //当前配置文件中会自动包含config目录下base.tsconfig.json中的所有配置信息
    "extends": "./configs/base.tsconfig.json",
    //指定被编译的文件列表，只有需要编译的文件少时才会用到
    //列表中的文件都会被TS编译器所编译
    "files": [
         "1.ts",
         "2.ts"
     ],
    "compilerOptions": {
        //target 用来指定被编译的ts的版本
        //ES3（默认）、ES5、ES6/ES2015、ES7/ES2016、ES2017、ES2018、ES2019、ES2020、ESNext
        "target": "ES5",   
        //设置编译后代码使用的模块化系统
        //CommonJS、UMD、AMD、System、ES2020、ESNext、None
        "module": "System",
        //指定代码运行时所包含的库（宿主环境）
        //ES5、ES6/ES2015、ES7/ES2016、ES2017、ES2018、ES2019、ES2020、ESNext、DOM、WebWorker、ScriptHost 
        "lib":["ES6", "DOM"],
        //outDir  用来指定编译后文件所在目录
        //默认情况下，编译后的js文件会和ts文件位于相同的目录，设置outDir后可以改变编译后文件的位置
        "outDir":"./dist",
        //将代码合并到一个文件
        //默认会将所有的编写在全局作用域中的代码合并为一个js文件，如果module制定了None、System或AMD则会将模块一起合并到文件之中
        "outFile": "./dist/app.js"，
    //指定代码的根目录，默认情况下编译后文件的目录结构会以最长的公共目录为根目录，通过rootDir可以手动指定根目录
        "rootDir":"./src/",
        
        编译生成相关设置
         //是否对js文件编译,默认是false
        "allowJs": false,
        //是否检查js代码是否规范
        "checkJs":false,
        //是否对注释进行编译
        "removeComments":false,
        //不生成编译文件，只是单纯为了检查语法
        "noEmit":false,
        //错误的文件不编译,编译更加严格
        "noEmitOnError": true，
        
        严格编译语法相关设置  
        //启用所有的严格检查，默认值为true，设置后相当于开启了所有的严格检查
        "strict":true,
        //用来设置编译后的文件是否使用严格模式，默认为false
        //但是其实有导入模块的代码时自动进入严格模式
        "alwaysStrict": true,
        //禁止隐式的any类型
        "noImplicitAny":true,
        //禁止类型不明确的this
        "noImplicitThis":true,
        //严格的空值检查
        "strictNullChecks":true,
        //严格检查属性是否初始化
        "strictPropertyInitialization":false,
        //严格检查函数的类型
        "strictFunctionTypes":false,
        //严格检查bind、call和apply的参数列表
        "strictBindCallApply":false
    }
}
```

### 5. webpack打包调试代码

通常情况下，实际开发中我们都需要使用构建工具对代码进行打包，TS同样也可以结合构建工具一起使用，下边以webpack为例介绍一下如何结合构建工具使用TS。

1. **初始化项目**

   进入项目根目录，执行命令 ``` npm init -y```

   主要作用：创建package.json文件

2. **下载构建工具**

   #### ```npm i -D webpack webpack-cli webpack-dev-server typescript ts-loader clean-webpack-plugin html-wepback-plugin``` 

   - **webpack**	构建工具webpack
   - **webpack-cli**	webpack的命令行工具
   - **webpack-dev-server**	webpack的开发服务器
   - **typescript**	ts编译器
   - **ts-loader**	ts加载器，用于在webpack中编译ts文件的
   - **html-webpack-plugin**	webpack中html插件，用来自动创建html文件
   - **clean-webpack-plugin** 	webpack清除插件，每次构建先清除目录

3. **根目录下创建webpack.config.js**

   ```json
   //引入一个包
   const path = require('path')
   const HTMLWebpackPlugin = require('html-webpack-plugin')
   const { CleanWebpackPlugin } = require('clean-webpack-plugin')
   
   //webpack中所有配置信息都应该写在moudle.exports中
   module.exports = {
   
       //指定入口文件
       entry: './src/index.ts',
       //指定打包文件所在目录
       output: {
           //指定打包文件的目录
           path: path.resolve(__dirname, 'dist'),
           //打包后的文件名字
           filename: 'bundle.js',
           //告诉webpack不适用箭头函数
           environment: {
               arrowFunction: false
           }
       },
       mode: 'development',
       //指定webpack打包时需要的模块
       module: {
           //指定要加载的规则
           rules: [{ //test指定的是规则生效的文件
               test: /\.ts$/,
               //要使用的loader
               use: [{
                       loader: 'babel-loader',
                       options: {
                           //设置预定义的环境
                           presets: [
                               //指定环境的插件
                               ["@babel/preset-env",
                                   //配置信息
                                   {
                                       //要兼容的目标浏览器
                                       "targets": {
                                           "chrome": "58",
                                           "ie": "11"
                                       },
                                       //指定corejs的版本
                                       "corejs": "3",
                                       //使用corejs的方式 “usage”表示按需加载
                                       "useBuiltIns": "usage"
                                   }
                               ]
                           ]
                       }
   
                   },
                   { loader: 'ts-loader' }
               ],
               //要排除的文件
               exclude: /node_modules/
           }]
       },
       //配置wepback插件
       plugins: [
           new CleanWebpackPlugin(),
           new HTMLWebpackPlugin({
               template: './src/index.html'
           }),
       ],
       //用来设置 可以引用的模块
       resolve: {
           extensions: ['.ts', '.js']
       }
   }
   ```

4.  **根目录下创建tsconfig.json,配置可以根据自己需要**

   ```json
   {
       "compilerOptions": {
           "target": "ES2015",
           "module": "ES2015",
           "strict": true
       }
   }
   ```

5.  **修改package.json添加如下配置**

   ![1646568503357](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646568503357.png)

6. **在src下创建ts文件，并在并命令行执行```npm run build```对代码进行编译，或者执行```npm start```来启动开发服务器**

### 6.Babel

经过一系列的配置，使得TS和webpack已经结合到了一起，除了webpack，开发中还经常需要**结合babel来对代码进行转换以使其可以兼容**到更多的浏览器，在上述步骤的基础上，通过以下步骤再将babel引入到项目中。

```npm i -D @babel/core @babel/preset-env babel-loader core-js```

1. **安装依赖包**

   4个包分别是：

   - **@babel/core**	bebel的核心工具
   - **@babel/preset-env**	babel的预定义环境
   - **@babel-loader**	babel在webpack中的加载器
   - **core-js**	core-js用来使老版本的浏览器支持新版ES语法

2. 修改webpack.config.js

   ```js
   module: {
       //指定要加载的规则
       rules: [{ //test指定的是规则生效的文件
           test: /\.ts$/,
           //要使用的loader
           use: [{
               loader: 'babel-loader',
               options: {
                   //设置预定义的环境
                   presets: [
                       //指定环境的插件
                       ["@babel/preset-env",
                        //配置信息
                        {
                            //要兼容的目标浏览器
                            "targets": {
                                "chrome": "58",
                                "ie": "11"
                            },
                            //指定corejs的版本
                            "corejs": "3",
                            //使用corejs的方式 “usage”表示按需加载
                            "useBuiltIns": "usage"
                        }
                       ]
                   ]
               }
   
           },
                 { loader: 'ts-loader' }
                ],
           //要排除的文件
           exclude: /node_modules/
       }]
   },
   ```

   如此一来，使用ts编译后的文件将会再次被babel处理，使得代码可以在大部分浏览器中直接使用，可以在配置选项的targets中指定要兼容的浏览器版本。

## 二、面向对象

### 类

面向对象是程序中一个非常重要的思想，它被很多同学理解成了一个比较难，比较深奥的问题，其实不然。面向对象很简单，简而言之就是程序之中所有的操作都需要通过对象来完成。

举例来说：

- 操作浏览器要使用window对象
- 操作网页要使用document对象
- 操作控制台要使用console对象

```ts
//使用class关键词来定义一个类

class Person{
    //定义实例的属性
    name:string='刘强'
    age:number=18
    //定义静态属性
    static sender:string = '男'
    //定义只读属性,无法修改
    readonly school:string = '南昌大学'
    //定义只读的类的属性,无法修改
    static readonly live:boolean = true

    constructor(name:string,age:number){
        this.name =name
        this.age =age
    }
    //实例方法
    sayHello(){
        console.log(this.age)
    }

    //静态方法
    static saybye(){
        console.log("bye")
    }
}

const per = new Person('刘强',24)
console.log(Person.sender)
Person.saybye()
per.sayHello()
```

### 继承

```js
//父类
class Animals{
    name:string;
age:number;
constructor(name:string,age:number){
    this.name=name
    this.age=age
}
sayHello(){
    console.log('jiaojiaojiao')
}
}
//子类
class Dog extends Animals{
    constructor(name:string,age:number){
        super(name,age)
    }
    sayHello(){
        console.log('wangwangwang')
    }
}   

//子类
class Cat extends Animals{
    sender:string
    constructor(name:string,age:number,sender:string){
        //如果子类写了构造函数，那么在子类构造函数中必须对父类构造函数进行调用！！
        super(name,age)
        this.sender=sender
    }
//重写父类方法
	sayHello(){
    console.log('miaomiaomiao')
}
}   


const d = new Dog('旺财',2)
const m = new Cat('吴云',2)
console.log(d)
d.sayHello()
m.sayHello()
```

### 抽象类

**以abstract开头的类是抽象类**，区别不大，只是不能创建对象，就是被继承的！

**以abstract开头的方法是抽象方法**，没有方法体，**只能定义在抽象类中，子类必须对他进行重写。**

```ts
//抽象类
abstract class Animal{
    name:string;
    constructor(name:string){
        this.name=name
    }
    //抽象方法
    abstract sayHello():void
}

class Dog1 extends Animal{
    constructor(name:string){
        super(name)
    }
    sayHello(){
        console.log('wangwangwang')
    }
}   

const d1 = new Dog1('旺财')
console.log(d1)
d1.sayHello()
```

### 接口

接口就是用来定义一个类的结构，和抽象类不同在**接口中的所有方法和属性都是没有实值**的。换句话说**接口中的所有方法都是抽象方法**。

接口可以去限制一个对象的接口，对象只有包含接口中定义的所有属性和方法时才能匹配接口。同时，可以让一个类去实现接口，实现接口时类中要保护接口中的所有属性。

**当类型来用**

类型只能单个声明，接口可以声明多个

```ts
type myType={
    name:string,
    age:number
}
const obj:myType={
    name:'liuqiang',
    age:24
}

interface MyInterface{
    name:string,
    age:number
}
interface MyInterface{
    sender:string
}
const obj1:MyInterface={
    name:'liuqiang',
    age:24,
    sender:'男'
}
```

**检查对象类型**



```ts
interface Person{
    name: string;
    sayHello():void;
}

function fn(per: Person){
    per.sayHello();
}

fn({name:'孙悟空', sayHello() {console.log(`Hello, 我是 ${this.name}`)}});
```

**实现**

定义类是， 可以使一个类实现接口：**就是让类满足接口的要求**

```ts
interface myInter{
    name:string
    age:number
    sayHello():void
}

class MyClass implements myInter{
    name:string
    age: number
    constructor(name:string,age: number){
        this.name=name
        this.age=age
    }
    sayHello(){
        console.log(this.name,this.age)
    }
}
```

### 属性封装

对象实质上就是属性和方法的容器，它的主要作用就是存储属性和方法，这就是所谓的封装。对象的属性是可以任意的修改的，为了确保数据的安全性，在TS中可以对属性的权限进行设置

**只读属性（readonly）：**

​		如果在声明属性时添加一个readonly，则属性便成了只读属性无法修改

TS中属性具有三种修饰符：

- **public**（默认值），可以在类、子类和对象中修改
- **protected** ，可以在类、子类中修改
- **private** ，可以在类中修改

```ts
class Person1{
    //public 可以在任意位置进行访问
    public _name:string
    //private 私有属性 只能在类内部进行访问 需要通过添加方法来设置
    private _age:number
    //protected 可以在当前类和子类进行访问
    protected sender:string
    constructor(name:string,age:number){
        this._name=name
        this._age=age
    }

    //获取
    getAge(){
        return  this._age
    }
    //设置
    setAge(age:number){
        this._age =age
    }
}
let p1 = new Person1('liuqiang',123)
console.log(p1._name)
// console.log(p1.age)//属性“age”为私有属性，只能在类“Person1”中访问
console.log(p1.getAge())


class A extends Person1{
    test(){
        console.log(this.sender)
    }
}

const a = new A('asd',123,'nan')
a.test()//男
a.sender ='nv'//报错 实例不行只能类和子类中进行访问
```

### 属性存取器

对于一些不希望被任意修改的属性，可以将其设置为private,将导致无法再通过对象修改其中的属性。

我们可以在**类中定义一组读取、设置属性的方法称为属性的存取器**。读取属性的方法叫做setter方法，设置属性的方法叫做getter方法

```ts
class Person1{
    //private 私有属性 只能在类内部进行访问 需要通过添加方法来设置
    private _age:number
    constructor(age:number){
        this._age=age
    }
    
    //ts中getter简便方法
    get age(){
        return this._age
    }
    set age(value:number){
        this._age=value
   }

}

let p1 = new Person1(23)
//ts简便方法
p1.age=1223
console.log(p1.age)
```

### 属性定义快捷方法

语法糖

```ts
class A{
    constructor(public name:string,public age:number){
        this.name = name
        this.age = age
    }
}

等同于
class A{
    name:string
    age:number
    constructor( name:string, age:number){
        this.name = name
        this.age = age
    }
}

```

### 泛型

定义一个函数或类时，有些情况无法确定具体的类型（返回值、参数、属性的类型不能确定），这时候需要泛型

```ts
======================案例1=======================
//定义函数或是类时，遇到不类型不明确可以使用泛型

function fn<T>(a:T):T{
    return a
}

//可以直接调用具有泛型的函数

console.log(fn(12))//不指定泛型 ts会自动对类型进行推断
console.log(fn<String>('刘强'))//指定泛型
======================案例2=======================
function fn2<T,K>(a:T,b:K):T{
    console.log(b)
    return a
}

fn2<number,string>(123,'hello')

======================案例3=======================
interface Inter{
    name:string
}
//T extends Inter 表示泛型T必须是inter实现类（子类）
function fn3<T extends Inter>(a:T):string{
    return  a.name
}
fn3({name:'asd'})

======================案例4=======================
class myClass<T>{
    constructor(public name:T){
        this.name =name
    }
}
const  c= new myClass<string>('liu')
```

