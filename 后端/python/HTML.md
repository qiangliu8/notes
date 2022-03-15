# HTML

### HTML

- HTML (Hypertext Markup Language) 超文本标记语言。
- 它负责王爷的三个要素之中的结构。
- HTML使用标签的形式来标识网页中的不同组成部分。
- 所谓超文本指的是**超链接**，使用超链接可以让我们从一个页面跳转至另一个页面。

### 标签

<head>是网页的头部，head中的内容不会在网页中直接出现，主要用来帮助浏览器或搜索引擎来解析网页
<meta> 标签用来设置网页的元数据，设计网页的字符集，防止乱码问题
<title> 中的内容会显示在浏览器的标题栏，搜索殷勤会主要根据title中的内容来判断网页的主要内容
<body> html的子元素，表示网页的主体，网页中所有的可见内容都用写在body里

### 实体

如果我们需要在网页中书写特殊符号，需要使用html中实体（转义字符）

![image-20211023170943197](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211023170943197.png)

### meta标签

```html
<!--页面介绍-->
<meta name="description" content="这是我的网站的自我介绍">
<!--跳转页面--> 
<meta http-equiv="refresh" content="3; url=https://www.baidu.com">
```

##### \<blockquote>和\<q>

```html
<blockquote>长引用，会有进行缩进效果,会独占一行</blockquote>
<q>短引用，会自动加引号,不会独占一行</q>
```

![image-20211025105307230](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211025105307230.png)

##### \<strong>和\<em>的区别

\<strong>表示语气加重，语义内容重要

\<em>标签用于表示语音语调的一个加重

#### 定义列表

**使用dl标签创建一个定义列表**

**使用dt来表示定义的内容**

**使用dd来对内容进行解释说明**

```html
<dl>
    <dt>俞文竹</dt>
    <dd>刘强最爱的那个人啊 一直都很爱</dd>
    <dd>刘强的初恋</dd>
</dl>
```

![image-20211025151006939](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211025151006939.png)

#### 音视频播放

##### 音频文件

audio标签用来向页面引入一个外部的音频文件的。

音视频文件引入时，默认情况**不允许用户自己控制播放停止**。

**属性：**

**controls** 是否允许用户控制播放

**autoplay** 音频文件是否自动播放

​	如果设置了autoplay 则音乐在打开页面时会自动播放

​	但是目前来讲大部分浏览器都不会自动对音乐进行播放

**loop** 音频文件是否循环播放

```html
<audio src="./花海.mp3" controls autoplay loop></audio>
```

除了通过src来指定外部文件的路径外，还可以通过**source来指定文件**

```html
<audio controls>
    对不起，请升级浏览器哦！
    <source src="./花海.mp3">
    <embed src="./花海.mp3" type="audio/mp3" width="300">
</audio>
```

##### 视频文件

和音频文件同理

```html
<video controls autoplay loop>
    <source src="../../../迅雷下载/怪奇物语.Stranger.Things.S01E01.中英字幕.WEB-HR.AAC.1024X576.x264.mp4">
</video>
```

### 文档流

文档流 网页是一个多层的结构，一层一层。通过CSS可以分别为每一层来设置样式。作为用户来讲只能看到最顶上一层。

这些层中，最底下的一层称为**文档流**，文档流是网页的基础。我们所创建的元素默认都是在文档流中进行排列。

两种状态：

- **在文档流中**

  块元素会在页面中独占一行(自上向下垂直排列)

  默认宽度是父元素的全部(会把父元素撑满)

  默认高度是被内容撑开(子元素)

- **脱离文档流**

  行内元素不会独占页面的一行，只占自身的大小
  行内元素在页面中左向右水平排列，如果一行之中不能容纳下所有的行内元则元素会换到第二行继续自左向右排列（书写习惯一致)
  行内元素的默认宽度和高度都是被内容撑开

文档流中：

- **块元素**

  块元素会在页面中独占一行(自上向下垂直排列)

  默认宽度是父元素的全部（会把父元素撑满)

  默认高度是被内容撑开（子元素)

- **行内元素**

  行内元素不会独占页面的一行，只占自身的大小

  行内元素在页面中左向右水平排列，如果一行之中不能则元素会换到第二行继续自左向右排列(书写习惯一-

  行内元素的默认宽度和高度都是被内容撑开

### 盒子模型

#### 块状元素的盒模型

内边距：内容去和边框之间的距离是内边距。

内边距的设置会影响到盒子的大小，背景颜色会延伸到内边距上。

![image-20211106144541854](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211106144541854.png)

**盒子的大小=内容区+内边距+边框   的大小**

所以在计算盒子大小时，需要将这三个区城加到一起计算

外边距：外边距不会影响盒子可见框的大小，但是外边距会影响盒子的位置。



一个元素在其父元素中，水平布局必须要满足以下的等式
margin-left+borden-left+padding-left+width+padding-right+border-right+margin-right = 其父元素内容区的宽度（必须满足)

0+0+0 + 200+0+0 +0 =800 

以上等式必须满足，如果相加结果使等式不成立，则称为**过渡约束**，则等式会自动调整-调整的情况:

**-如果这七个值中没有为 auto的情况，**则浏览器会自动调整margin-right值以使等式满足

0+0+0 + 200 +0+0 + 600 = 800

**-这七个值中有三个值和设置为auto**

如果某个值为auto，则会自动调整为auto的那个值以使等式成立

0+0+0 + auto + 0 +0+0 = 800	auto = 800

0+0+0 + auto +8 +0 + 200 = 800	auto = 800

200 +0+0 + auto + 0+0 + 200 = 800	auto = 400

![image-20211106151749956](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211106151749956.png)

#### 外边距的折叠

##### 兄弟元素间

```html
.box1 {
    background: red;
    margin-bottom: 100px;
}
.box2 {
    background: green;
    margin-bottom: 30px;
}

<div class="box1"></div>
<div class="box2"></div>
```

相邻元素的**垂直方向的外边距**会发生折叠现象

**兄弟元素间**的相邻垂直外边距会取两者之间的较大值（都是正值或都是负值），假如一正一负，取二者之和。不需要进行处理

##### 父子元素间

父子元素间相邻外边距，子元素的会传递给父元素(上外边距)

父子外边距的折叠会影响到页面的布局，必须要进行处理

![image-20211106153952390](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211106153952390.png)

```html
.box3 {
    background: red;
}

.box4 {
    background: green;
    margin-top: 120px;
}

<div class="box3">
    <div class="box4"></div>
</div>
```

#### 行内元素的盒模型

行内元素不只是设置宽度和高度，但是可以改内外边距  

行内元素可以设置padding，但是垂直方向padding不会影响页面的布局

行内元素可以设置border，垂直方向的border不会影响页面的布局

行内元素可以设置margin，垂直方向的margin不会影响布局

**display用来设置元素显示的类型**

可选值：

​		inline将元素设置为行内元素block将元素设置为块元素

​		inline-block将元素设置为行内块元素 行内块，既可以设置宽度和高度又不会独占一行

​		table 将元素设置为一个表格

​		none元素不在页面中显示

**visibility用来设置元素的显示状态**

​	可选值:

​		visible默认值，元素在页面中正常显示

​		hidden元素在页面中隐藏不显示，但是依然占据页面的位置

#### 盒子大小

默认情况下，盒子可见框的大小由内容区、内边距和边框共同决定。

**box-sizing**:用来设置盒子尺寸的计算方式，设置width和height

可选项：

​		**content-box**：默认值，宽度和高度用来设置内容区的大小=内容区

​		**boder-box**：宽度和高度用来设置整个可见框的大小=内容区+内边距+边框 	

## 表格		

普通表格

```html
<table>
    <tr>
        <td>日期</td>
    </tr>
</table>
```

长表格

```html
<table>
    <thead>
        <tr>
            <td>日期</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>200.01</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td></td>
        </tr>
    </tfoot>
</table>
```

#### 表格样式

```css
table{
	border-spacing:0px; //指定边框的距离
	border-collapse:collapse;//设置边框的合并
}
```

```css
/* 如果表格中没有使用tbody而是直接使用tr
那么浏览器会直接创建一个tbody,并且将tr全部放到tbody中
tr不是table的子元素，是tbody的子元素 */
tbody>tr:nth-child(odd) {
    background: yellow;
}
```



# CSS

## 选择器

### 父选择器 关系选择器

**div+q** 选择紧跟 <div> 元素的首个 <p> 元素。

**p~ul** 选择前面有 <p> 元素的每个 <ul> 元素。

**div>q** 选择div的孩子中的q 不是所有的q

### 属性选择器

[属性名]选择含有指定属性的元素

[属性名=属性值]选择含有指定属性和属性值的元素

[属性名^=属性值]选择属性值以指定值开头的元素

[属性名$=属性值]选择属性值以指定值结尾的元素

[属性名*=属性值]选择属性值含有指定值的元素

```html
p[title=123]{
	color:red
}
p[title^=12]{
	color:red
}


<p title="123">p</p>
```

### 伪类选择题

::afer 伪元素

:after 伪类

伪类（不存在的类，特殊的类）：

​		伪类用来描述一个元素的**特殊状态**，比如第一个子元素，被点击的元素

#### child伪类

​		**:first-child** 第一个子元素

​		**:last-child **最后一个子元素

​		**:nth-child** 第n个子元素

​			特殊值 

​				**n**  第n个n的范围0到正无穷

​				**2n 或 even** 表示选中偶数位的元素

​				**2n+1 或 odd**表示选中奇数位的元素

```css
//列表li里第一个子元素
ul>li:first-child(2n) {
	color: red;
}
```

​	**必须是父元素的第一个元素，如下否则无效**

```html
ul>li:first-child {
color: red;//失效
}

<ul>
    <span>123</span>
    <li>one</li>
    <li>two</li>
    <li>three</li>
</ul>
```

#### :not 否定伪类

```css
//ul的li都是红色 除了第一个元素
ul>li:not(:first-child) {
    color: red;
}
```

### 伪元素选择器

伪元素：表示页面中一些特殊的**并不真实**的存在的元素

**::first-letter** 表示第一个字母

**::first-line** 表示第一行

**::selection** 表示选中的内容

**::before** 元素的开始

**::after** 元素的最后

```css
p::first-letter{
    font-size:20px
}

p::selection{
    background-color:pink  
} 

//before和after必须配合content使用
p::before{
    content: '"';
    color: red;
}
p::after{
    content: '"';
    color: red;
}
```



### 超链接的伪类

**:link** 用来表示没访问过的链接

**:visited** 用来表示访问过的链接 只能修改颜色

**:hover** 用来表示鼠标放入的状态

#### 选择器的权重

样式的冲突：当我们通过不同的选择器，选中相同的愿随，去并且为相同样式设置不同的值时，此时就发生样式的冲突。

发生样式冲突时，应用哪个样式由选择器的权重（优先级）决定



|     选择器     |       权重       |
| :------------: | :--------------: |
|    内联样式    |     1,0,0,0      |
|    id选择器    |     0,1,0,0      |
| 类和伪类选择器 |     0,0,1,0      |
|   元素选择器   |     0,0,0,1      |
|   通配选择器   |     0,0,0,0      |
|   继承的样式   |    没有优先级    |
|   !important   | 最高优先级，慎用 |



## 继承

样式的继承，我们为一个元素设置的样式同时也会**应用到它的后代上。**不仅是儿子

```html
p{
	color:red
}

<p>
	123
	<span>111</span>
    <!-- span和p都会变成红色 -->
</p>
```

继承是发生在祖先和后代之间的

继承的设计是为了方便开发，利用继承可以将一些通用的样式同意设置到共同的祖先元素上。

但是**背景，布局相关样式不会被继承。**

## 单位

#### 像素

-屏幕（显示器）实际上是由一个一个的小点点构成的

-不同屏幕的像素大小是不同的，像素越小的屏幕显示的效果越清晰-所以同样的200px在不同的设备下显示效果不一样

#### 百分比

-也可以将属性值设置为相对于其父元素属性的百分比-设置百分比可以使子元素跟随父元素的改变而改变

#### em

em是相对于元素的字体大小来计算的- 

1em = 1font-size

em会根据字体的大小改变而改变

```css
p{
	font-size:30px;
	width:10em;
	height:10em;<!-- 10em = 300px -->
}
```

#### rem

rem是根据根元素的字体大小来计算

```css
html{
	font-size:20px;
}
p{
	width:10em;
	height:10em;<!-- 10em = 200px -->
}
```

## 颜色单位

在CSS中可以直接使用**颜色名**来设置各种颜色。

比如:red、orange、yellow、blue、green ..... .但是在css中直接使用颜色名是非常的不方便

**RGB值:**

RGB通过三种颜色的不同浓度来调配出不同的颜色- 

R red，G green , B blue

每一种颜色的范围在0 - 255 (O% - 108%）之间-

语法:RGB(红色,绿色,蓝色)

**RGBA:**

就是在rgb的基础上增加了一个a表示不透明度

**十六进制的RGB值:**

语法:#红色绿色蓝色

颜色浓度通过06-ff

如果颜色两位两位重复可以进行简写#aabbcc --> #abc

**HSL值**

​	H	色相

​	S	饱和度，颜色的浓度 0%-100%

​	L	亮度，颜色的亮度 0%-100%

```css
background-color: red;
background-color: Orgb(255，0，0);
background-color: rgb(e，255,0);
background-color: Orgb(e，0，255);
background-color: rgb(255,255,255);
background-color:rgb(106,153,85);
background-color:rgba(106,153,85,.5）;
background-color:#ffe8B0;
background-color: #ffff00;
background-color: #ff0;
background-color:#bfa;
background: hsl(120, 20%, 39%)
```

### 边框

#### 轮廓

outline用来设置元素的轮廓线，用法和boder一摸一样。

轮廓和边框不同的点，就是轮廓不会影响可见框的大小。

```css
outline: 10px red solid;
```

#### 阴影

用来设置元素的阴影效果，阴影不会影响页面布局

```css
box-shadow:2px 3px black;
//第一参数 水平偏移量 设置阴影的水平位置，正值向右移动，负值向左移动
//第二参数 垂直偏移量 设置阴影的垂直位置，正值向下移动，负值向上移动
//第三参数 阴影的模糊半径
//第四参数 阴影颜色
```

#### 圆角

用来设置圆角园角设置的圆的半径大小

四个值 左上	右上 右下	左下

三个值 左上	右上/左下	右下

两个值 左上/右下	右上/左下	

```
boder-radis：
```

### 浮动

通过浮动可以使一个元素向其父元素的左侧或右侧移动

使用float 属性来设置于元素的浮动
	可选值:

​	none 默认值﹐元素不浮动

​	left 元素向左浮动

​	right 元素向右浮动

注意,元素设置浮动以后，水平布局的等式**便不需要强制成立**

元素设置浮动以后，会完全**从文档流中脱离，不再占用文档流的位置**，所以元素下边的还在文档流中的元素会自动向上移动

#### 浮动特点

- 浮动元素会完全脱离文档流，不再占据文档流中的位置

- 设置浮动以后元素会向父元素的左侧或右侧移动

- 浮动元素默认不会从父元素中移出

- 浮动元素向左或向右移动时，不会超过它前边的其他浮动元素

- **如果浮动元素的上边是一个没有浮动的块元素，则浮动元素无法上移**

- 浮动元素不会超过它上边的浮动的兄弟元素，最多最多就是**和它一样高**

- **浮动元素不会盖住文字，文字会自动环绕在浮动元素的周围**,所以我们可以利用浮动来设置文字环绕图片的效果

- 元素设置浮动以后，将从文档流脱离，特点也会发生变化。

  文档流脱离特点：

  **块元素：**

  1. 块元素不在独占页面一行
  2. 不设置宽高，默认块元素的宽度和高度默认被内容撑开

  **行内元素：**

  ​	行内元素脱离文档流以后会变成块元素，特点和块元素一样

  **总而言之，脱离文档流之后，不区分行内和块元素了！！！**

### 定位

定位是一种更加高级的布局手段

通过定位可以将元素摆放到页面的任意位置

使用position属性来设置定位

可选值:

​	**static**默认值，元素是静止的没有开启定位

​	**relative**开启元素的相对定位

​	**absolute**开启元素的绝对定位

​	**fixed** 开启元素的固定定位

​	**sticky**开启元素的粘滞定位

#### 相对定位:

当元素的position属性值设置为relative时则开启了元素的相对定位

**是相对于自己之前的位置，还占着之前的位置**

相对定位的特点:

元素开启相对定位以后，如果不设置偏移量元素不会发生任何的变化

#### 绝对定位

当元素的position属性值设置为absolute时，则开启了元素的绝对定位

绝对定位的特点:

1. 开启绝对定位后，如果不设置偏移量元素的位置不会发生变化
2. 开启绝对定位后，元素会从文档流中脱离
3. 绝对定位会改变元素的性质，行内变成块，**块的宽高被内容撑开**
4. 绝对定位会使元素提升一个层级
5. 绝对定位元素是相对于其**包含块**进行定位的

**包含块**( containing block )，正常情况下:

包含块就是离当前元素最近的祖先块元素

```
<div><span><em>hello</em></span></div>
```

绝对定位的包含块:

​	包含块就是离它最近的开启了定位的祖先元素，

​	如果所有的祖先元素都没有开启定位则根元素就是它的包含块

​	html（根元素、初始包含块)

#### 固定定位

将元素的position**属性设置为fixed**则开启了元素的固定定位

固定定位也是一种绝对定位，所以固定定位的大部分特点都和绝对定位一样

唯一不同的是固定定位**永远参照于浏览器的视口**进行定位

固定定位的元素**不会随网页的滚动条滚动**

#### 粘滞定位

当元素的position属性设置为sticky时则开启了元素的粘滞定位

粘滞定位和相对定位的特点基本一致，

不同的是粘滞定位可以在元素**到达某个位置时将其固定**

兼容性不好不推荐

```css
ul {
    position: sticky;
    top: 20px;
}
```



### 字体

可以直接将服务器中的字体直接提供给用户![image-20211111112334820](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211111112334820.png)

```css
@font-face{
    /* 指定字体的名字 */
    font-family:'myfont' ;
    /* 服务器中字体的路径 */
    src: url(.....);
}

p{
    font-family: myfont
}
```

问题：加载速度慢、版权

### 图标

FontAwesome

**第一种方式**-引入类的方式

```css
<link rel="stylesheet" href="./css/all.css">


<i class="fas fa-bell"></i>
```

**第二种方式**-引入尾元素的方式

```css
li::before {
    content: '\f1b0';
    font-family: 'Font Awesome 5 Free';
    font-weight: 900;
    color: red;
}
```

**第三种方式**-引入实体的方式

```html
<span class="fa">&#xf0f3;</span>
```

#### 背景

```css
.box {
    width: 500px;
    height: 500px;
    background-color: #bfa;
    
    /* background-image设置背景图片
    可以同时设置背景图片和背景颜色，这样背景颜色将会成为图片的背景色
    如果背景的图片小于元素，则背景图片会自动在元素中平铺将元素铺满
    如果背景的图片大于元素，将会一个部分背景无法完全显示 */
    background-image: url("./大黄猫/dahuangmao-04.png");
    
    /* background-repeat用来设置背景的重复方式
    可选值:
    repeat 默认值﹐背景会沿着x轴 y轴双方向重复
    repeat-x沿着x轴方向重复
    repeat-y沿着y轴方向重复工
    no-repeat背景图片不重复 */
    background-repeat: no-repeat;
    
    background-position: center;
    /* background-size: 100% 100%; */
}
```

##### 背景的范围

```css
.box {
    width: 500px;
    height: 500px;
    background-color: #bfa;
    background-image: url("./大黄猫/dahuangmao-04.png");
    background-repeat: no-repeat;
    background-position: center;
 
    /* background-clip
    可选值:
    border-box默认值，背景会出现在边框的下边
    padding-box背景不会出现在边框，只出现在内容区和内边距
    content-box背景只会出现在内容区 */
    background-clip: border-box;
    
    border: 10px red double;
}
```

##### 图片原点偏移

```css
.box {
    width: 500px;
    height: 500px;
    background-color: #bfa;
    background-image: url("./大黄猫/dahuangmao-04.png");
    border: 10px red double;
    /* background-origin背景图片的偏移量计算的原点
    padding-box默认值，
    background-position从内边距处开始计算
    content-box背景图片的偏移量从内容区处计算 
    border-box 背景图片的偏移量从边框开始计算*/
    background-origin: content-box;

    /*background-attachment
    背景图片是否跟随元素移动-可选值:
    scroll 默认值背景图片会跟随元素移动
    fixed背景会固定在页面中，不会随元素移动 */
    background-attachment: fixed;
}
```

注意:

**background-size必须写在background-position的后边，并且使用/隔开**

background-position/background-size

**background-origin background-clip两个样式，orgin要在clip的前边** 

#### 雪碧图

```css
<style>
a:link {
    display: block;
    width: 93px;
    height: 30px;
    background-image: url('./按钮/btn.png');
}

a:hover {
    background-position: -93px 0;
}

a:active {
    background-position: -186px 0;
}
</style>
```

##### 解决图片闪烁的问题：

可以将多个小图片同意保存到一个大图片，然后通过调整background-position来显示

这样图片会同时加载到网页中就可以有效的避免出现闪烁的问题

这个技术在网页中应用十分广泛，被称为cSs-Sprite。这种图我们称为雪碧图

##### 雪碧图的使用步骤;

1. 先确定要使用的图标
2. 测量图标的大小
3. 根据测量结果创建一个元素
4. 将雪碧图设置为元素的背景图片
5. 设置一个偏移量以显示正确的图片

### 渐变

通过渐变可以设置一些复杂的背景颜色，可以实现从一个颜色向其他颜色过度的效果。**渐变是图片，需要通过background-image来设置。**

线性渐变，颜色沿着一条直线发生变化。

**linear-gardient()**

-线性渐变的开头，我们可以指定一个渐变的方向

to left

to right

to bottom

to top

deg deg表示度数

turn表示圈

渐变可以指定多个颜色，默认情况下平均分布。

```css
background-image: linear-gradient(to left, red, yellow);
background-image: linear-gradient( red 150px, yellow);
```

![image-20211115132927651](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211115132927651.png)

**repeating-linear-gardient()** 可以平铺的线性渐变

```csss
background-image: repeating-linear-gradient(red 20px, yellow 40px);
```

![image-20211115133656277](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20211115133656277.png)

**radial-gradien**t镜像渐变

默认情况下径向渐变的形状根据元素的形状来计算的

正方形-->圆形

长方形-->椭圆形
我们也可以手动指定径向渐变的大

circle

ellipse

也可以指定渐变的位置

```
 background-image: radial-gradient(100px 100px at top, red, yellow);
```

