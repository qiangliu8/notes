# Python入门

[TOC]



## 1.pycharm安装

### 模板

**增加自动模板，创建文件时自动生成注释**

模板案例：

```python
#-*- coding = utf-8 -*-              设置编译格式是utf-8
#@Time : ${DATE} ${TIME}			 设置文件创建时间
#@Author : 刘强						展示文件创作者
#@File : ${NAME}.py					 展示置文件名
#@Software : ${PRODUCT_NAME}		 展示编译器软件
```

样例截图：

![image-20210628101620622](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210628101620622.png)

### 添加注释

```
#单行注释

'''
这是第一行注释
这是第二行注释
'''
```

## 2.入门基础

### 变量及类型

变量可以是**任意的数据类型**，在程序钟用一个变量名表示

变量名必须是**大小写英文、数字和下划线**的组合，且不能以数字开头

赋值(a='ABC')时，Python解释器干了两件事：

1. 在内存中创建一个‘ABC’的字符串
2. 在内存中创建一个名为a的变量，并把它指向‘ABC’

### 关键字

python中具有特殊功能的标识符，不允许来发这自己定义**和关键字相同名字**的标识符

查看关键字：

```python
import keyword
print(keyword.kwlist)

['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']

```

### 格式化输出

```python
age = 23
name = '刘强'
print("我的年纪是:%d岁"%age)
print("我的年纪是:%d岁,姓名是%s" % (age,name))

print('www','baidu','com',sep='.')
www.baidu.com
```

#### 常用的格式符号

![image-20210628131657204](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210628131657204.png)

#### 换行输出

```python
print("hello",end="")
print("python",end='\t')
print("hello",end='\n')
print("world",end='\n')
hellopython	hello
world
```

### 输入

```python
>>> a = input() 
123 
>>> a 123 
>>> type(a) 
<type 'int'> 
>>> a = input() 
abc 
Traceback (most recent call last): 
    File "<stdin>", line 1, in <module> 
    File "<string>", line 1, in <module> 
NameError: name 'abc' is not defined 
>>> a = input() 
"abc" 
>>> a 
'abc' 
>>> type(a) <type 'str'> 
>>> a = input() 
1+3 
>>> a 
4
>>> a = input() 
"abc"+"def" 
>>> a 
'abcdef' 
>>> value = 100 
>>> a = input() 
value 
>>> a 100
```

### 运算符和表达式

![image-20210628150448394](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210628150448394.png)

![image-20210628150456060](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210628150456060.png)

![image-20210628150624227](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210628150624227.png)

![image-20210628150630104](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210628150630104.png)

![image-20210628150637866](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210628150637866.png)

![image-20210628150646052](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210628150646052.png)

![image-20210628150653317](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210628150653317.png)

## 3.判断语句和循环语句

#### 条件判断语句

![image-20210628160919895](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210628160919895.png)

```python
if age>=18: 

print "我已经成年了"


score = 77 
if score>=90 and score<=100: 
    print('本次考试，等级为A') 
elif score>=80 and score<90: 
    print('本次考试，等级为B')
elif score>=70 and score<80: 
    print('本次考试，等级为C') 
elif score>=60 and score<70: print('本次考试，等级为D') 
    #elif score>=0 and score<60: 
else: #elif可以else一起使用 
    print('本次考试，等级为E')
```

#### import 与 from...import

在python用**import**或者**from...import**来导入相应的模块

在A模块导入，格式应为import A

从A模块导入某个B函数，格式应为 from A import B

从A模块导入某个B,C函数，格式应为 from A import B,C

将A模块的全部函数导入，格式应为 form A import *

【生成随机数】

1. 第一行代码引入库：

   ```python
   import  random
   ```

2. 生成指定范围的随机数

   ```python
   print(random.randint(0,2))
   ```



### 循环语句

#### for循环

![image-20210629111420012](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210629111420012.png)

#### for循环的格式

```python
for 临时变量 in 列表或字符串等
 	循环满足条件时执行的代码
    
name = 'chengdu' 
for x in name: 
    print(x)
```

### while循环

![image-20210629114601566](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210629114601566.png)

```python
i = 0 
while i<5: 
	print("当前是第%d次执行循环"%(i+1)) 
	print("i=%d"%i) 
	i+=1
```

break和countine

![image-20210629120145244](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210629120145244.png)

```python
i = 0 
while i<10: 
	i = i+1 
	print('----') 
	if i==5: 
		break 
	print(i) 

i = 0 
while i<10: 
    i = i+1 
    print('----') 
    if i==5: 
        continue 
    print(i)
```

## 4.字符串、列表、元组、字典

### 字符串

![image-20210629181047737](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210629181047737.png)

```python
word = '这是字符串'
sentence = "这是句子"
paragraph = '''这是段落
    可以换行
    不信你试试
'''

print(word)
print(sentence)
print(paragraph)

这是字符串
这是句子
这是段落
    可以换行
    不信你试试
```

#### 单引号和双引号如何选择

1. **包含单引号的字符串**

   假如你想定义一个字符串my_str，其值为： I'm a student，则可以采用如下方式，通过转义字符 \ 进行定义。

   ```python
   my_str='I\'m student'
   ```

   也可以不使用转义字符，利用双引号直接进行定义。

   ```python
   my_str = "I'm a student"
   ```

2. 包含双引号的字符串

   假如你想定义一个字符串my_str，其值为： Jason said "I like you" ，则可以采用如下方式，通过转义字符 \ 进行定义。

   ```python
   my_str = "Jason said \"I like you\""
   ```

   也可以不使用转义字符，利用单引号直接进行定义。

   ```python
   my_str = 'Jason said "I like you"'
   ```

#### 转义字符

![image-20210629182420626](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210629182420626.png)

#### 字符串的截取和链接

```python
str='chengdu' 

print(str) 				# 输出字符串 
print(str[0:-1]) 		# 输出第一个到倒数第二个的所有字符 
print(str[0]) 			# 输出字符串第一个字符 
print(str[2:5]) 		# 输出从第三个开始到第五个的字符 
print(str[2:]) 			# 输出从第三个开始后的所有字符 
print(str * 2) 			# 输出字符串两次 print(str + '你好') # 连接字符串 
print(str[:5]) 			# 输出第五个字母前的所有字符 
print(str[0:7:2]) 		# [起始：终止：步长] 
print('------------------------------') 
print('hello\nchengdu') # 使用反斜杠(\)+n转义特殊字符 
print(r'hello\npython') # 在字符串前面添加一个 r，表示原始字符串，不会发生转义
```

#### 字符串的常见操作

![image-20210629184217097](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210629184217097.png)

## 5.列表

![image-20210629185558357](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210629185558357.png)

#### 列表的定义与访问

##### 列表的格式

变量A的类型为列表

```python
namesList = ['xiaoWang','xiaoZhang','xiaoHua']
```

比C语言的数组强大的地方在于列表中的元素可以是不同类型

**列表中可以存储混合类型**

```python
testList = ['liuqiang', 'is', 23]
```

##### 打印列表

```python
testList = ['liuqiang', 'is', 23]
print(testList[0])
print(testList[1])
print(testList[2])
```

为了更有效率的输出列表的每个数据，可以使用循环来完成

```python
for i in testList:
    print(i)
```

#### 常用操作

![image-20210630110328837](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210630110328837.png)

#### 列表的嵌套

**列表嵌套**

类似while循环的嵌套，列表也是支持嵌套的

一个列表中的元素又是一个列表，那么这就是列表的嵌套

```python
schoolNames = [['北京大学','清华大学'], 
				['南开大学','天津大学','天津师范大学'], 
				['山东大学','中国海洋大学']]
```

```python
nameList = ['liuqiang', 'is', '666']
nameList1 = ['yuwenzhu', 'is', '888']

#增
nameList.append(nameList1)#追加是在末尾整体加入
nameList.extend(nameList1)#追加是在末尾依次加入
nameList.insert(1,3)	  #指定下标位置插入元素
print(nameList)
['liuqiang', 3, 'is', '666', ['yuwenzhu', 'is', '888'], 'yuwenzhu', 'is', '888']

#查 ----记住左闭右开
print(nameList.index('666',2,5)) #查找[0,3)下标范围内有没有3这个变量 并且告诉你的下标 3
print(nameList.count('666'))# 统计元素出现次数 1


#删
del nameList[1]#指定位置删除一个元素
nameList.pop()#弹出末尾最后一个元素
nameList.remove("666")#直接删除指定位置的元素，只删除第一个 第二个就不删除了

print(nameList)
['liuqiang', 'is', ['yuwenzhu', 'is', '888'], 'yuwenzhu', 'is']


#反转
nameList.reverse()
print(nameList)
['is', 'yuwenzhu', ['yuwenzhu', 'is', '888'], 'is', 'liuqiang']

```

### 元组--不可修改！

![image-20210630130832755](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210630130832755.png)

#### 元组的定义与访问

##### 元组的定义

```python
tup1 = ()  # 创建空的元组
tup2 = (50) #这是整型 不是元组 # 不加逗号，类型为整型
tup3 = (50,) # 加逗号，类型为元组
print(type(tup1))
print(type(tup2))
print(type(tup3))

<class 'tuple'>
<class 'int'>
<class 'tuple'>
```

##### 元组的访问

```python
tup1 = ('Google', 'baidu', 2000, 2020) 
tup2 = (1, 2, 3, 4, 5, 6, 7 ) 
print ("tup1[0]: ", tup1[0]) 
print ("tup2[1:5]: ", tup2[1:5])
```

**元组中的元素值是不允许修改的，但我们可以对元组进行连接组合，如下实例**

```python
tup1 = (12, 34.56) 
tup2 = ('abc', 'xyz') 
# 以下修改元组元素操作是非法的。 
# tup1[0] = 100 
# 创建一个新的元组 
tup3 = tup1 + tup2 
print (tup3)
```

**删除元组后，再次访问会报错**

```python
tup = ('Google', 'baidu', 2000, 2020) 
print (tup) 
del tup 
print ("删除后的元组 tup : ") 
print (tup)
```

#### 常用操作

![image-20210630134203370](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210630134203370.png)

### 字典

![image-20210630134448089](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210630134448089.png)

#### 字典的定义

变量info为字典类型：

```python
info={'name':'刘强','age':18}
```

1. 字典和列表一样，也能够存储多个数据

2. 列表中找某个元素时，是根据下标进行的

3. 字典中找某个元素时，是根据'名字'（就是冒号:前面的那个值，例如上面代码中

   的'name'、'id'、'sex'）

4. 字典的每个元素由2部分组成，键:值。例如 'name':'班长' ,'name'为键，'班长'为值

#### 根据键访问值

```python
print(info['name'])
刘强

print(info['sex']) #直接访问会报错 获取不存在的key，会发生异常

print(info.get('sex')) # 获取不存在的key，获取到空的内容，不会出现异常
None

print(info.get('sex','男')) #若info中不存在'sex'这个键，就返回默认值，找到显示原值
男
```

#### 常规操作![image-20210630144221812](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210630144221812.png)

```python
#增
info['id']=411016620343
print(info)
{'name': '刘强', 'age': 18, 'id': 411016620343}

#删 clear
info.clear()
print(info)
{}

#del
del info['id']#删除了指定键值对后·再次访问会报错
print(info)
{'name': '刘强', 'age': 18}

#查
print(info.keys())
dict_keys(['name', 'age', 'id'])

print(info.values())
dict_values(['刘强', 18, 411016620343])

#遍历所有键值对
for key,value in info.items():
    print("key=%s,value=%s" %(key,value))
    
key=name,value=刘强
key=age,value=18
key=id,value=411016620343

#使用枚举函数，同事拿到列表中的下标和元素内容
for i,j in enumerate(info):
    print(i,j)

```

### 集合

![image-20210705093224367](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210705093224367.png)

### 常用操作

![image-20210705094009968](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210705094009968.png)

### 小结

![image-20210705094144688](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210705094144688.png)

## 6.函数

如果在开发程序时，需要某块代码多次，但是为了提高编写的效率以及代码的重用，所以把具有独

立功能的代码块组织为一个小模块，这就是函数。

### 函数定义和调用

```python
def 函数名(): 
	代码
# 定义完函数后，函数是不会自动执行的，需要调用它才可以 
printInfo()
```

### 函数参数

```python
def add2num(a, b): 
	c = a+b 
	print c 
add2num(11, 22) 
#调用带有参数的函数时，需要在小括号中，传递数据
```

### 函数返回多个值

```python
def divid(a, b):
	shang = a//b 
	yushu = a%b 
	return shang, yushu 
sh, yu = divid(5, 2) 
```

### 局部变量和全局变量

#### 局部变量

![image-20210705102230328](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210705102230328.png)

#### 全局变量

如果一个变量，既能在一个函数中使用，也能在其他的函数中使用，这样的变量就是 全局变量

```python
# 定义全局变量 
a = 100 
def test1(): 
	print(a) 
def test2(): 
	print(a) 
# 调用函数 
test1() 
test2()
```

![image-20210705103801569](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210705103801569.png)

#### 修改全局变量

global a表示申明函数内该变量用的是不再是局部变量还是全局变量

![image-20210705112607207](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210705112607207.png)

## 7.文件操作

### 文件打开与关闭

在python，使用open函数，可以打开一个已经存在的文件，或者创建一个新文件

​	open(文件名，访问模式)

```python
f =open('1.txt','w')
f.close()
```

![image-20210706100325930](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210706100325930.png)

### 文件读写

#### 写数据

使用write()可以完成向文件写入数据

```python
f = open('test.txt', 'w') 
f.write('hello world, i am here!') 
f.close()
```

如果文件不存在那么创建，如果存在那么就先清空，然后写入数据

#### 读数据（read）

使用read(num)可以从文件中读取数据，num表示要从文件中读取的数据的长度（单位是字节），如果

没有传入num，那么就表示读取文件中所有的数据

```python
f = open('test.txt', 'r') 
content = f.read(5) 
print(content) 
print("-"*30) 
content = f.read() 
print(content) 
f.close() 
```

如果open是打开一个文件，那么可以不用写打开的模式，即只写 open('test.txt')

如果使用读了多次，那么后面读取的数据是从上次读完后的位置开始的

就像read没有参数时一样，readlines可以按照行的方式把整个文件中的内容进行一次性读取，并且返

#### 读数据（readlines）

就像read没有参数时一样，readlines可以按照行的方式把整个文件中的内容进行一次性读取，并且返回的是一个列表，其中每一行的数据为一个元素

```python
#coding=utf-8 
f = open('test.txt', 'r') 
content = f.readlines() 
print(type(content)) 

i=1 
for temp in content: 
	print("%d:%s"%(i, temp)) 
	i+=1
f.close() 
```

#### 读数据（readline）

```python
#coding=utf-8 
f = open('test.txt', 'r') 
content = f.readline() 
print("1:%s"%content) 
content = f.readline() 
print("2:%s"%content) 
f.close() 
```

### 文件的相关操作

有些时候，需要对文件进行重命名、删除等一些操作，python的os模块中都有这么功能

#### 文件重命名

os模块中的rename()可以完成对文件的重命名操作

**rename(原文件名,新文件名)**

```python
import os 
os.rename("毕业论文.txt", "毕业论文-最终版.txt")
```

#### 删除文件

os模块中的remove()可以完成对文件的删除操作

**remove(待删除的文件名)**

```python
import os 
os.remove("毕业论文-最终版.txt")
```

#### 创建文件夹

```python
import os 
os.mkdir("yu")
```

#### 获取目录列表

```python
import os 
print(os.listdir("./"))
['.idea', '1.txt', 'demo1.py', 'demo2.py', 'demo3.py', 'demo4.py', 'demo5.py', 'liuqiang.txt', 'main.py', 'venv', 'yu']

```

#### 删除文件夹

```python
import os 
os.rmdir('yu')
```

## 8.错误与异常

### 异常简介

![image-20210706195629775](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210706195629775.png)

![image-20210706195701580](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210706195701580.png)

### 捕获异常

```python
try:
    print("-------1-----")
    f = open("122.txt",'r')
    print("-------2-----")
except IOError:
    pass


-------1-----
```

此程序看不到任何错误，因为用except 捕获到了IOError异常，并添加了处理的方法

pass 表示实现了相应的实现，但什么也不做；如果把pass改为print语句，那么就会输出其他信息

![image-20210706200603046](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210706200603046.png)

### except捕获多个异常

```python
try:print 
	num 
except IOError: 
	print('产生错误了')
```

上例程序，已经使用except来捕获异常了，为什么还会看到错误的信息提示？

except捕获的错误类型是IOError，而此时程序产生的异常为 NameError ，所以except没有生效

修改后的代码为:

```python
try:
    print(num)
except NameError:
    print('产生错误了')
```

实际开发中，捕获多个异常的方式，如下：

```python
#coding=utf-8 
try:
	print('-----test--1---') 
	open('123.txt','r') # 如果123.txt文件不存在，那么会产生 IOError 异常 
	print('-----test--2---') 
	print(num)# 如果num变量没有定义，那么会产生 NameError 异常 
except (IOError,NameError): 
	#如果想通过一次except捕获到多个异常可以用一个元组的方式
```

当捕获多个异常时，可以把要捕获的异常的名字，放到except 后，并使用元组的方式仅进行存储

### 获取异常的信息描述

![image-20210706202016505](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210706202016505.png)

### 捕获所有异常

![image-20210706202418972](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210706202418972.png)

### try...finally

try...fifinally...语句用来表达这样的情况：

在程序中，如果一个段代码必须要执行，即无论异常是否产生都要执行，那么此时就需要使用

fifinally。 比如文件关闭，释放锁，把数据库连接返还给连接池等

```python
import time

try:
    f = open('1.txt','r')
    try:
        while True:
            content = f.readline()
            if len(content) == 0:
                break
            time.sleep(2)
            print(content)
    finally:
        f.close()
        print('文件关闭')
except Exception as result:
    print('发生异常')
```

test.txt文件中每一行数据打印，但是我有意在每打印一行之前用time.sleep方法暂停2秒钟。这样

做的原因是让程序运行得慢一些。在程序运行的时候，按Ctrl+c中断（取消）程序。

我们可以观察到KeyboardInterrupt异常被触发，程序退出。但是在程序退出之前，fifinally从句仍

然被执行，把文件关闭。

## 9.爬虫工作

### 准备工作

#### 编码规范

![image-20210707095924944](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210707095924944.png)

#### 引入模块

![image-20210707095637157](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20210707095637157.png)

**模块** **module**：一般情况下，是一个以.py为后缀的文件。

module 可看作一个工具类，可共用或者隐藏代码细节，将相关代码放置在一个module以便让代码更好用、易懂，让coder重点放在高层逻辑上。

module能定义函数、类、变量，也能包含可执行的代码。module来源有3种：

①Python内置的模块（标准库）；

②第三方模块；

③自定义模块。

**包** **package**： 为避免模块名冲突，Python引入了按目录组织模块的方法，称之为 包（package）。包是含有Python模块的文件夹。

```python
from bs4 import BeautifulSoup #网页解析，获取数据
import re   #证则表达是，进行文字匹配
import urllib.request,urllib.error  #判定url,获取网页数据
import xlwt   #进行execl操作 
import sqlite3  #进行SQL数据库操作
```

#### 获取数据

