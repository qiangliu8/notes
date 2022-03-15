# jQuery基础

[TOC]



## 一、jQuery概念

### 1.jQuery版本

![image-20220105163544602](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220105163544602.png)

### 2.jquery内部发生

```js
(function(){
    var jQuery = function (){
        return new xxx()
    }
    window.$= window.jQuery = jQuery
})(window)
```

## 二、jQuery的两个重要元素

**jQuery函数**（$/jQuery）:直接可用

```js
console.log($,typeof $)
console.log(jQuery ===$)
```

![image-20220105161537317](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220105161537317.png)

**jQuery对象**（$()/jQuery()返回的对象）：执行jQuery

```js
console.log($() instanceof Object ) //true
```

### 1.jQuery核心函数

#### 作为一般函数调用：$(param)

1. 参数为**函数**：当Dom加载完成后，执行此函数
2. 参数为**选择器字符串**：查找所有匹配的标签。并将他们封装成jQuery对象
3. 参数为**Dom对象**：将dom对象封装成jQuery对象
4. 参数为**html标签字符串**(用的少)：创建标签对象并封装成jQuery对象

```js
    $(function() { //1、绑定文档加载完成的监听
        $('#btn').click(function() { //2.参数为选择器字符串:查找所有匹配的标盈，并将它们封装成query对象
            this.innerHTML = 'anniu' //this是发生事件的dom元素 button 不是jq对象
            $(this).html("123") //3.参数为**Dom对象**：将dom对象封装成jQuery对象
            $('<input id="in" value="123" />').appendTo('html') //4.参数为**html标签字符串**(用的少)：创建标签对象并封装成jQuery对象
        })
    })
```

#### 作为对象去使用：$.xxx()

1. $.each()：隐式遍历数组

   ```js
   var arr = [2, 4, 7]
   $.each(arr, function(index, item) {
       console.log(index, item)
   })
   0 2
   1 4 
   2 7
   ```

2. $.trim()：去除两端的空格

   ```js
   var name = ' liu qiang '
   console.log($.trim(name))
   ```

### 2.jQ核心对象

**即执行jQuery核心函数返回的对象**

jQuery对象内部包含的是dom元素对象的**伪数组**(可能只有一个元素)

jQuery对象拥有很多有用的属性和方法，让程序员能方便的操作dom

#### 属性/方法

![image-20220106124137486](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220106124137486.png)

#### 基本行为

![image-20220106123425002](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220106123425002.png)

1.统计有多少个按钮

```js
var  buttons = $("button")
//size() / length 包含的dom元素的个数
console.log(buttons.length, button.size())
```

2.取出第二个button的文本

```js
//[index] /get(index) 得到对那个位置的dom元素
console.log(buttons[1].innerHTML, buttons.get(1).innerHTML)
```

3.输出所有button标签的文本

```js
//each() 遍历包含的所有dom元素
btutons.each(function(index,domfile){
    console.log(index,domfile.innerHTML,this)
})
```

![image-20220106131329242](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220106131329242.png)

each遍历的出都是dom元素

4.输出'按钮2'按钮是所有按钮的第几个

```js
console.log($('#btn2').index())
```



**伪数组**

```js
var  weiArr = {}
weiArr.length = 0
weiArr[0]='qiang'
weiArr.length = 1
weiArr[1]='zhu'
weiArr.length = 2

for (var i = 0;i<weiArr.length;i++){
    var obj = weiArr[i]
    console.log(i,obj)
}
```

因为伪数组，所以数组方法不可用

```js
console.log(buttons instanceof Array) false
console.log(buttons.foEach, weiArr.forEach) underfined
```

## 三、jQuery核心函数

### 1.选择器

#### 说明

选择器本身只是一个**有特定语法规则**的字符串，没有实质用处

它的基本语法规则使用的就是**CSS的选择器语法**，并对基进行了扩展只有调用$，并将选择器作为参数传入才能起作用

$ (selector)作用：根据选择器规则在整个文档中查找**所有匹配的标签的数组**，并封装成jQuery对象

#### 分类

![image-20220106161847417](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220106161847417.png)

##### 基本选择器

![image-20220106162118553](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220106162118553.png)



```html
<body>
    <div id="div1" class="box">div1(class="box")</div>
    <div id="div2" class="box">div2(class="box")</div>
    <div id="div3">div3</div>
    <span class="box">span(class='box')</span>
    <br/>
    <ul>
        <li>AAAAAAAAAA</li>
        <li title="hello">BBBBBBBBB(title="hello")</li>
        <li class="box">CCCCCCCCCCC(class="box")</li>
        <li title="hello">DDDDDDDDD(title="hello")</li>
    </ul>
</body>
```

选择id为div1的元素

```js
$("#div1").css('background','yellow')
```

选择所有的div元素

```js
$("div").css('background','blue')
```

选择所有class属性为box的元素

```js
$(".box").css('background','pink')
```

选择所有的div和span元素

```js
$("div,span").css('background','black')
```

选择所有class属性为box的div元素

```js
$("div.box").css('background','red')
```

##### 层次选择器

![image-20220106162206169](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220106162206169.png)

层次选择器:**查找子元素，后代元素，兄弟元素的选择器**

1. ancetor descendant
在给定的祖先元素下匹配所有的后代元素
2. parent>child
    在给定的父元素下匹配所有的子元素
3. prev+next
    匹配所有紧接在 prev元素后的next元素
4. prev~siblings
    匹配prev元素之后的所有siblings元素



```html
<body>
    <ul>
        <li>AAAAAAAAAA</li>
                <li class="box">CCCCCCCCCCC</li>
        <li title="hello"><span>BBBBBBBBB</span>span></li>
        <li title="hello"><span>DDDDDDDDD</span></li>
        <span>EEEEE</span>
    </ul>
</body>
```

选中ul下所有的的span

```js
$("ul span").css('background','pink')
```

选中ul下所有的子元素span

```js
$("ul>span").css('background','red')
```

选中class为box的下一个li

```js
$(".box +li").css('background','blue')
```

选中ul下的class为box的元素后面的所有兄弟元素

```js
$("ul .box ~ *").css('background','yellow')
```

##### 过滤选择器

![image-20220106162428925](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220106162428925.png)



![image-20220106203436011](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220106203436011.png)

选择第一个div

```js
$('div:first').css("background",'pink')
```

选择最后一个class为box的元素

```js
$('.box:last').css("background",'pink')
```

选择所有class属性不为box的div

```js
$('div:not(.box)').css("background",'pink')
```

选择第二个和第三个li元素

```js
这是根据索引
$('li:gt(0):lt(2)').css("background",'pink')
$('li:lt(3):gt(0)').css("background",'pink')
```

选择内容为BBBBB的li

```js
$('li:contains("BBBBB")').css("background",'pink')
```

选择隐藏的li

```js
$('li:hidden).css("background",'pink')
```

选择有title属性的li元素

```js
$('li[title]').css("background",'pink')
```

选择所有属性title为hello的li元素

```js
$('li[title=hello]').css("background",'pink')
```

##### 表单选择器

![image-20220106162549206](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220106162549206.png)

选择不可用的文本输入框

```js
$(":text:disabled")
```

显示选择爱好的个数的多选框

```js
$(":checkbox:checked")
```

显示下拉选择的城市名称

```js
$("option:selected").html()
```

### 2.$.工具的方法

each():遍历数组或对象中的数据

```js
var obj = {
    name:'liu',
    age:18
}
$.each(obj,function(key,value){
    console.log(key,value)
})
```

trim():去除字符串两边的空格

type( obj):得到数据的类型

```js
console.log($.type($))  'function'
```

isArray(obj):判断是否是数组

```js
console.log($.isArray($('body')))  'false'
console.log($.isArray([1,2]))  'true'
```

isFunction(obj):判断是否是函数

```js
console.log($.isFunction($)  'true'
```

parseJSON(json) :解析json字符串转换为js对象/数组

```js
var json = '{"name":"liu","age":12}'
json对象转为js对象
console.log($.parseJSON(json)) {name: 'liu', age: 12}

JSON.parse(jsonString) json字符串---》js对象/数组
JSON.stringify(jsObj) js对象数组--》json字符串
```

### 3.属性

读取第一个div的title属性

```js
$("div:first").attr('title')
```

给所有的div设置name属性(value为liu)

```js
$("div").attr('name','liu')
```

移除所有div的title属性

```js
$("div").remove('title')
```

给所有的div设置cLass='liuclass '

```js
$("div").attr('class','liuclass ')
```

给所有的div添加cLass='abc'

```js
$("div").addClass('abc ')
```

**移除所有div的liucLass 的class**

```js
$("div").remove("liucLass")
```

得到最后一个Li的标签体文本

```js
$("li:last").html()
```

设置第一个Li的标签体为"<h1>mmmmmmmmm</ h1>"

```js
$("li:first").html("<h1>mmmmmmmmm</ h1>")
```

得到输入框中的vaLue值

```js
$(":text").val()
```

将输入框的值设置为liu

```js
$(":text").val("liu")
```

点击'全选'按钮实现全选

```js
var checkboxs = $(":checkbox")
$("button:first").click(function(){
	checkboxs.attr('checked',true)
})
```

点击'全不选'按钮实现全不选

```js
var checkboxs = $(":checkbox")
$("button:last").click(function(){
	checkboxs.attr('checked',fal
})
```

### 4.CSS

#### css()

得到第一个p标签的颜色

```js
$('p:first').css('color')
```

设置所有p标签的文本颜色为red

```js
$('p').css('color','red')
```

设置第2个p的字体颜色(#ff0011),背景(blue)，宽(30epx)，高(30px)

```js
$('p:eq(1)').css({
    color:;f0011,
    background:'blue',
    width:300,
    height:30
})
```

#### 位置 

##### offset和position

![image-20220107160034908](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220107160034908.png)

打印div1相对于页面左上角的位置

```js
var offset = $('#div1').offset()
console.log(offset.left, offset.top)
```

打印div2相对于页面左上角的位置

```js
var offset = $('#div2').offset()
console.log(offset.top,offset.left)
```

打印div1相对于父元素左上角的位置

```js
var position = $('#div1').position()
console.log(position.top,position.left)
```

打印 div2相对于父元素左上角的位置

```js
var position = $('#div2').position()
console.log(position.top,position.left)
```

设置div2相对于页面的左上角的位置

```js
$('#div1').offset({
    left:50,
    top:100
})
```

##### scroll

得到div或者页面滚动条的坐标

```js
$("#divs").scrollTop()
```

##### 回到顶部

瞬间滚到底部

```js
$("html,body").scrollTop(0)
```

平滑到顶部

```js
//总距离
var distance = $("html,body").scrollTop()
//总时间
var time = 500
//间隔时间
var intervervalTime = 10
var itemDistance = distance / (time / intervervalTime)
//使用循环定时器不断滚动
var intervalId = setInterval(function() {
    if (distance <= 0) {
        distance = 0
        clearInterval(intervalId)
    }
    distance -= itemDistance
    $("html,body").scrollTop(distance)
}, intervervalTime)
```

#### 尺寸

![image-20220108124552694](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220108124552694.png)



内容尺寸

```js
$('div').width(), $('div').height()  100 150
```

内部尺寸

```js
$('div').innerWidth(), $('div').innerHeight() 120 170
```

外部尺寸

outerHeight(false/true):height+padding+border **如果是true 加上margin**

outerWidth(false/true):height+padding+border **如果是true 加上margin** 

```js
$('div').outerWidth(),$('div').outerHeight() 140 190
$('div').outerHeight(true),$('div').outerWidth(true) 160 210
```

### 5.筛选

#### 过滤

ul下li标签第一个

```js
var lis = $("ul>li")
lis.first() jq对象
lis[0] dom对象
```

ul下li标签的最后一个

```js
var lis = $("ul>li")
lis.last()
```

ul下li标签的第二个

```js
var lis = $("ul>li")
lis.eq(1)
```

ul 下li标签中title属性为hello的

```js
var lis = $("ul>li")
lis.fiter('[title=hello]')
```

ul 下li标签中title属性不为hello的 

```js
var lis = $("ul>li")
lis.not('[title!=hello]')
lis.fiter('[title!=hello]')
```

ul下li标签中有span子标签的

```js
var lis = $("ul>li")
lis.has('span')
```

#### 查找

![image-20220108191907270](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220108191907270.png)

ul标签的第2个span**子标签**

```js
var uls = $("ul")
uls.children('span:eq(1)')
```

ul标签的第2个span**后代标签**

```js
var uls = $("ul")
uls.find('span:eq(1)')
```

ul标签的父标签
```js
var uls = $("ul")
uls.parent()
```

id为cc的li标签的前面的所有li标签
```js
var li = $("#cc")
li.preAll('li')
```

id为cc的li标签的所有兄弟li标签
```js
var li = $("#cc")
uls.siblings('li')
```

#### 增删改

向id为ul1的ul下添加一个span(**最后**)

```js
var $ul = $('#ul1')
$ul.append('<span>append添加的span</span>')

$('<span>append添加的span</span>').appendTo($ul)
```

向id为ul1的ul下添加一个span(**最前**)
```js
var $ul = $('#ul1')
$ul.prepend('<span>prepend添加的span</span>')

$('<span>prepend添加的span</span>').prependTo($ul)
```

在id为ul1的ul下的li(title为hello)的前面添加span
```js
var $li = $('#ul1').children('li[title=hello]')
$li.before('<span>before添加的span</span>')
```

在id为ul1的ul下的li(title为hello)的后面添加span将
```js
var $li = $('#ul1').children('li[title=hello]')
$li.after('<span>after添加的span</span>')
```

在id为uL2的ul下的li(title为hello)全部替换为p
```js
var $li = $('#ul2').children('li[title=hello]')
$li.replaceWith('<p>replace</p>')
```

移除id为ul2的ul下的所有Li
```js
$('#ul2>li').remove()
```

### 6.事件处理

给.out绑定点击监听(用两种方法绑定)

```js
$('.out').click(function(){

})

$('.out').on('click',function(){
    
})
```

给.inner绑定鼠标移入和移出的事件监听(用3种方法绑定)
```js
$('.inner').mouseenter(function(){

}).mouseleave(function(){

})

$('.inner').on('mouseenter',function(){

}).on('mouseleave',function(){

})

$('.inner').hover(function(){
    console.log('移入')
},function(){
    console.log('移出')
})
```

点击btn1**解除**.inner上的所有事件监听
```js
$('.btn').click(function(){
	$('.inner').off()
})
```

点击btn2解除.inner上的mouseleave事件
```js
$('.btn2').click(function(){
	$('.inner').off('mouseleave')
})
```

点击btn3得到事件坐标

| 事件的坐标 |                                                   |
| ---------- | ------------------------------------------------- |
|            | event.clientX, event.clientY  相对于视口的左上角  |
|            | event.pageX, event.pageY  相对于页面的左上角      |
|            | event.offsetX, event.offsetY 相对于事件元素左上角 |

```js
$('.btn3').click(function(event){
    console.log(event.offsetX,event.offsetY) //原点为事件元素的左上角
    console.log(event.clientX,event.clientY) //原点为窗口的左上角
    console.log(event.pageX,event.pageY) //原点为页面的左上角
})
```

**停止事件冒泡 : event.stopPropagation()**  

**阻止事件默认行为 : event.preventDefault()**

点击.inner区域，外部点击监听不响应

```js
$('.inner').click(function(event){
    //停止事件冒泡
	event.stopPropagation()
})
```

点击链接，如果当前时间是偶数不跳转
```js
$('.out').click(function(event){
	if(Date.now()%2===0){
        event.preventDefault()
    }
})
```

#### mouseover和mouseenter的区别

mouseover在移入子元素时也会触发，对应mouseout

mouseenter只在移入当前元素时才会触发，对应mouseleave

**hover使用的是mouseenter和mouseleave**

#### on添加的click和click的区别

 jq的on可以添加多个 click也可以

### 7.事件委托

 新增的元素的点击事件覆盖不到，所以需要事件委托

- 将多个子元素li的事件监听委托给父辈元素ul处理
- 监听回调是加载父元素上
- 当操作任何一个元素li时，事件会冒泡的父辈元素
- 父辈元素不会直接处理事件，而是根据event.target得到发生的子元素li,操作这个子元素。这样有新的元素出现，自动会有事件响应处理

**设置事件委托: $(parentSelector).delegate(childrenSelector, eventName, callback)**

**移除事件委托: $(parentSelector).undelegate(eventName)**

![image-20220108213851621](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220108213851621.png)



```js
$('ul').delegate('li', 'click', function () {
    // console.log(this)
    this.style.background = 'red'
})

$('#btn1').click(function () {
    $('ul').append('<li>新增的li....</li>')
})

$('#btn2').click(function () {
    // 移除事件委托
    $('ul').undelegate('click')
})
```

### 8.效果

#### 淡入淡出

不断改变元素的透明度

fadeIn()淡入

fadeOut()淡出

fadeToggle() 切换淡入淡出

```js
$(function() {
    $('#btn1').click(function() {
        $('.div1').fadeIn(100)
    })
    $('#btn2').click(function() {
        $('.div1').fadeOut()
    })
    $('#btn3').click(function() {
        $('.div1').fadeToggle()
    })
})
```

#### 滑动

slideDown( ):带动画的展开

slideUp():带动画的收缩

slideToggle():带动画的切换展开/收缩

#### 显式隐藏

show():(不)带动画的显示

hide( ):(不)带动画的隐藏

toggle():(不)带动画的切换显示/隐藏

无参数就不带动画，**有参数就会有动画，参数是时间**

#### 自定义动画

![image-20220110154613489](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220110154613489.png)

**宽/高都扩为200px**

```js
$('#btn1').click(function() {
    $('.div1').animate({
        width: 200,
        height: 200
    }, 1000)
})
```

**移动到指定位置**

1. 移动到(500, 100)处
2. 移动到(100，20)处

```js
$('#btn2').click(function() {
    $('.div1').animate({
        top: 500,
        left: 100
    }, 1000).animate({
        top: 100,
        left: 20
    }, 1000)
})
```

**移动指定距离**

1. **移动距离为**(500, 100)
2. **移动距离为**(-100，-20)

```js
$('#btn3').click(function() {
    $('.div1').animate({
        top: '+=500',
        left: '+=100'
    }, 1000).animate({
        top: '-=100',
        left: '-=20'
    }, 1000)
})
```

**停止动画**

```js
$('#btn4').click(function() {
    $('.div1').stop()
})
```

### 9.多库共存

如果两个库都有$,就会存在冲突。

所以jQuery库可以释放$的使用权，让另一个库可以正常使用，此时jQuery库只能使用jQuery了。

API**:jQuery.noConflict()**



```js
<script src="mylib.js"></script>
<script src="jquery.js"></script>

<script>
    //释放$的使用权
        jQuery.noConflict()

	console.log($())
	console.log(jQuery())
</script>
```

![image-20220110171025568](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20220110171025568.png)

### 10.ready和onload的区别

```js
$(function(){
    
})
实际上就是
$(document).ready(function(){
    
})
```

测试方法

1. 直接打印img的宽度，观察其值
2. 在$(function(){})中打印img的宽度
3. 在 window.onLoad 中打印宽度
4. 在img加载完成后打印宽度

```js
console.log($('img').width())
//null

window.onload = function() {
    console.log('onload+',$('img').width())
}
//ready+ 0

$(function() {
    console.log('ready+',$('img').width())
})
//onload+ 242

<body>
    <img src="https://fc1tn.baidu.com/it/u=3420671844,3987300585&fm=202&mola=new&crop=v1" />
        </body>
```

由上面可以知道，

window.onload包括**页面图片加载完**才会执行回调，只能有**一个监听**。

ready而**页面加载完后**就回调，可以有**多个监听**。

## 四、jQuery插件

### 1.扩展插件

**给$添加4个工具方法**

- min(a,b)返回较小的值
- max(c,d)返回较大的值
- leftTrim()去掉字符串左右的空格
- rightTrim()去掉字符串左右的空格

**给jq对象添加3个功能方法**

checkAll()全选

unCheckAll()全不选

reverseCheck()全反选



my_jq_plugin.js

```js
(function() {
    $.extend({
        min: function(a, b) {
            return a < b ? a : b
        },
        max: function(a, b) {
            return a > b ? a : b
        },
        leftTrim: function(str) {
            return str.replace(/^\s+/, '')
        },
        rightTrim: function(str) {
            return str.replace(/\s+$/, '')
        },
    })
    $.fn.extend({
        checkAll: function() {
            //这里的this是jq对象
            this.prop('checked', true)
        },
        unCheckAll: function() {
            //这里的this是jq对象
            this.prop('checked', false)
        },
        reverseCheck: function() {
            //这里的this是jq对象
            this.each(function() {
                //这里的this是dom元素
                this.checked = !this.checked
            })
        }
    })
})()
```

index.html

```js
<script src="jquery.js"></script>

<script src="my_jq_plugin.js"></script>


console.log($.min(1, 2)) 1
console.log($.max(5, 2)) 5
console.log($.leftTrim("  asdasd    "))asdasd    
console.log($.rightTrim("  asdasd  "))  asdasd 
```

