# Vue

[TOC]

## 一、Vue核心

### 1.1初识 Vue

想让Vue工作，就必须创建一个Vue实例,且要传入一个配置对象;

root容器里的代码依然符html规范。只不过混入了一些特殊的Vue语法

root容器里的代码被称为【Vue模板】;

**容器一一对应！！只有一对一**

```vue
<body>
    <div id="root">
        <h1>你好,{{name}}</h1>
    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止vue在启动时生成生产提示

    //创建Vue实例
    const v = new Vue({
        el: "#root", //el用于指定当前vue实例为哪个容器服务 通常是css选择器
        data: { //data中用于存储数据，数据供el所指定的容器去使用，
            name: '刘强'
        }
    })
```

### 1.2 模板语法

html中包含了一些js语法代码，分为两种，分别为：

1. **插值语法(双大括号表达式)**
2. **指令语法(v-开头)**

#### 插值语法

用于解析标签体内容，**但是标签的属性不能用，就是href={{xxx}}是不行的**

语法： : {{xxx}} ，xxx 会作为 会作为js表达式解析

#### 指定语法

用于解析标签属性，解析标签体内容，绑定事件

举例：v-bind:href='xxxx',	xxxx会作为js表达式解析

可以省写成：

### 1.3 数据绑定

#### 单向数据绑定 v-bind

语法 v-bind:href

特点：数据只能从data流向页面

#### 双向数据绑定 v-model

**只能用于表单元素,默认收集value 所以简写可v-model**

语法：v-model:value="xxx" 或者v-model="xxxx"

特点数据不仅能从data流向页面，还能从页面流放data

```html
<body>
    <div id="root">
        <h2 >{{school}}</h2>
        <input v-model="school" />
    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止vue在启动时生成生产提示
    //创建Vue实例
    const v = new Vue({
        el: "#root", //el用于指定当前vue实例为哪个容器服务 通常是css选择器
        data: { //data中用于存储数据，数据供el所指定的容器去使用，
            school: '南昌大学'
        },
    })
</script>
```

#### el两种写法

```js
第一种写法
//创建Vue实例
const v = new Vue({
    el: "#root", 
})

第二种写法
const v = new Vue({})
v.$mount('#root')
```

#### data的两种写法

```js
第一种写法
//创建Vue实例
const v = new Vue({
    el: "#root", 
    data:{
        name:'刘强'
    }
})

第二种写法 这里不要写箭头函数 因为this指向会变成window
const v = new Vue({
    el: "#root", 
    data:funtion(){
        return{
            name:'刘强'
        }
    }
})

```

### 1.4 数据代理与Object.defineProperty

#### Object.defineProperty

defineProperty函数可以设置其他属性的值

```js
let person = {
    name: 'liuqiang',
    age: 12
}

//Object.defineProperty遍历的属性不可以枚举，并且不可修改
Object.defineProperty(person, 'sex', {
    value: '男',
    enumerable: false, //设置是否可以枚举，默认为false
    writable: true, //控制属性是否可以被修改，默认为false
    configurable: false //控制属性是否可以被删除，默认为false
})


console.log(person) //{name: 'liuqiang', age: 12, sex: '男'}

for (let key in person) {
    console.log(key) //name age
}
```

设置和访问属性时，调用getter、setter

**这样number就和object的属性就实现了动态绑定**

```js
let number = 23
let person = {
    name: 'liuqiang',
}

Object.defineProperty(person, 'age', {
    //当有人读取person的age属性时，get值会被调用，且返回值就是age的值
    get() {
        console.log('有人访问了age属性')
        return number
    },
    //当有人修改person的age属性时，set值会被调用，且会受到修改的具体值
    set(value) {
        console.log('有人设置了age属性')
        number = value
    }
})
```

![1646912466804](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646912466804.png)

#### 数据代理

通过一个对象代理对另一个对象中的属性的操作，读/写

```js
let o1 = {
    name: '刘强'
}
let o2 = {
    password: 123
}


Object.defineProperty(o1, 'password', {
    get() {
        return o2.password
    },
    set(value) {
        o2.password = value
    }
})

//o1不需要设置属性 通过访问o2进行代理
console.log(o1.password) //123
o2.password = 456
console.log(o1.password) //345
```

#### 用于vue中的数据绑定

通过obj.defineProperty()把data对象中的所有属性添加到vm上，为每一个添加到vm上的属性都指定一个getter、setter。在getter、setter内部去操作data中对象的值。直接代理到vm的_data上

![1646915617956](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646915617956.png)

#### Vue监测数据的原理

##### 监听器实现

实现一个数据劫持监听对象

```js
let data = {
    name: '刘强',
    age: 23
}

//创建一个监视的实例对象，用于监视data中属性的变化
function Observer(Obj) {
    const keys = Object.keys(Obj)
    keys.forEach(item => {
        Object.defineProperty(this, item, {
            get() {
                return Obj[item]
            },
            set(val) {
                Obj[item] = val
            }
        })
    })
}

const ob = new Observer(data)

vm._data = data = ob
```

##### Vue.set()实现响应式对象添加

同时需要添加Vue.set()进行添加对象。因为data只能进行数组绑定，对象里面还有属性，不能做到二次监听，所以需要Vue.set()

使**用Vue.set()为Vue._data中的stu对象添加一个属性**，这样这个属性也是响应式，也有get和set

```html

<div id="root">
    <button @click="addSex">addSex</button>
    <h2>学生名称：{{stu.name}}</h2>
    <h2>性别{{stu.sex}}</h2>
</div>

<script type="text/javascript">
    Vue.config.productionTip = false

    //创建Vue实例
    const v = new Vue({
        el: "#root",
        data: {
            stu: {
                name: 'tom',
            },
        },
        methods: {
            addSex() {
                Vue.set(this.stu, 'sex', '男')
            }
        },
    })
</script>
```

同时Vue.set() 是向响应式对象中添加一个property，并确保它要是响应式的。但是**不能添加到vm._data身上，必须是响应式对象对象身上。！！**不能是Vue实例，也不能是Vue实例的根数据对象

##### 监听数组实现

vm._data对象里的数组无法实现动态监听，例如：

![1647245966783](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1647245966783.png)

所以这个时候 给这个数组进行赋值是不管用的，但是vue自己有那种vue的数组写法,进行了数组封装。

#### 监听总结

![1647257018396](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1647257018396.png)

### 1.5 MVVM

![1646900658384](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646900658384.png)

![1646901579608](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646901579608.png)

### 1.6 事件处理

#### 绑定监听

- 使用v-on:xxx 或者@xxx 绑定事件，xxx是事件名
- 事件的回调需要配置在methods对象中，最终会在vm上
- methods中配置的函数，最好别用this。并且这**些函数都是被vue所管理的函数**，this的指向都是vm或者组件实例对象
- **@click=demo 和@click=demo($event) 效果一样，但是后者可以传参**

```js
<body>
    <div id="root">
        <h2 v-on:click="hello">点击</h2>
        <h2 @click="say(1,$event)">点击</h2>
    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止vue在启动时生成生产提示

    //创建Vue实例
    const v = new Vue({
        el: "#root", 
        data: () => {
            return { 
                school: '南昌大学'
            }
        },
        methods: {
            hello(e) {
                console.log(this) //这里是vue实例对象
                console.log(e.target)
            },
            //想要有event 就需要绑定时拿$event占位
            say(juzi, event) {
                alert(juzi)
            }
        }
    })
```

![1646918656442](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646918656442.png)

#### 事件修饰符

- **prevent**：阻止事件的默认行为 event.prevetDefault()
- **stop**：停止事件冒泡 event.stopPropagation()
- once：事件只触发一次
- capture：使用事件的捕获模式
- self：只有event.target是当前操作的元素才触发事件
- passive：事件的默认行为立即执行，无需等待事件回调执行完毕

```html
<body>
    <div id="root">
        <!-- 1.阻止事件跳转 -->
        <a href="www.baidu.com" @click.prevent="stoptiao">不可调转的百度链接</a>
        <!-- 2.阻止事件冒泡 -->
        <div id="body" @click="stopmaopao">
            <div id="clicks" @click.stop="stopmaopao"></div>
        </div>
        <!-- 3.只触发一次 -->
        <div id="clicks" @click.once="onceclick"></div>
        <!-- 4.事件捕获模式 -->
        <!-- 事件一般是先捕获再冒泡，加capture上捕获事件先处理 -->
        <div class="box1" @click.capture="showmsg(1)">
            box1
            <div class="box2" @click="showmsg(2)">
                box2
            </div>
        </div>
        <!-- 5.只有event.target是当前操作的元素才触发事件 -->
        <div id="body" @click.self="stopmaopao">
            <div id="clicks" @click="stopmaopao"></div>
        </div>
        <!-- 6.事件的默认行为立即执行，无需等待事件回调执行完毕 -->
        <!-- 先执行默认的滚动行为，再执行回调函数 -->
        <div @scroll.passive="demo" class="list">
            <li>1</li>
            <li>2</li>
            <li>3</li>
        </div>
    </div>
</body>


<script type="text/javascript">
    Vue.config.productionTip = false 
    //创建Vue实例
    const v = new Vue({
        el: "#root",
        methods: {
            stoptiao() {
                alert('我不跳转！')
            },
            stopmaopao() {
                alert('我不冒泡！')
            },
            onceclick() {
                alert('就一次！')
            },
            showmsg(msg) {
                alert(msg)
            },
            demo() {
                console.log(123)
            }
        }
    })
</script>
```

#### 按键修饰符

keycode：操作的是某个keycode值得键

keyName：操作的是某个按键名得键

<img src="C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646967536503.png" alt="1646967536503" style="zoom:67%;" />

### 1.7计算属性与监视

#### 计算属性

定义：要用属性不存在。**需要通过已有属性计算得来**

原理：底层调用了Object.defineproperty方法提供的getter和setter

.get函数什么时候执行?

1. **初次读取时会执行一次。**
2. **当依赖的数据发生改变时会被再次调用。**

优势：与method实现相比，内部有缓存机制，效率更高，调试放边。

注意：计算属性最终会**出现在vm**上，直接读取使用即可

**如果计算属性要被修改，那么必须写set函数去响应修改。且set要引起计算时依赖得数据发生变化！！！**

```html
<div id="root">
        姓：<input v-model:value="firstName" />名：<input v-model:value="lastName" />
        <!-- 使用插值语法拼接 -->
        <h1>{{firstName.slice(0,3 )}}-{{lastName}}</h1>
        <!-- 使用函数返回 -->
        <h1>{{fullname()}}</h1>
        <!-- 计算属性 -->
        <h1>{{fullName}}</h1>
    </div>

<script type="text/javascript">
    Vue.config.productionTip = false
    //创建Vue实例
    const v = new Vue({
        el: "#root",
        data: {
            firstName: '刘',
            lastName: '强'
        },
        computed: {
            fullName: {
                //get有什么作用，当有人读取就会调用get,且返回值作为fullname
                //初次访问时发生调用get，或者所依赖得数据发生变化
                get() {
                    console.log('读取了fullName')
                    return this.firstName + '-' + this.lastName
                },
                //被修改时调用
                set(value) {
                    console.log('修改了fullName')
                    let str = value.split('-')
                    this.firstName = str[0]
                    this.lastName = str[1]
                }
            }
        },
        methods: {
            //只要data数据改变，vue就会重新解析模板
            fullname() {
                return this.firstName + this.lastName
            }
        }
    })
</script>
```

**简写代码**

如果只读不写得话，那么不用设置set 并且get函数直接赋值给计算属性

```js
//创建Vue实例
const v = new Vue({
    el: "#root",
    data: {
        firstName: '刘',
        lastName: '强'
    },
    computed: {
        fullName: function() {
            return this.firstName + '-' + this.lastName
        }
    }
})
```

#### 监视属性

监视属性watch

1. 当被监视的属性变化时，回调函数自动调用，进行相关操作。
2. **监视的属性必须存在，才能进行监视**
3. 监视两种写法
   - new Vue 时传入watch配置
   - 通过vm.$watch配置

```html

<body>
    <div id="root">
        <h2>今天天气不错{{info}}</h2>
        <button @click="changes">切换</button>
    </div>
</body>

<script type="text/javascript">
    Vue.config.productionTip = false

    //创建Vue实例
    const v = new Vue({
        el: "#root",
        data: {
            isHot: true
        },
        computed: {
            info: function() {
                return this.isHot ? '炎热' : '凉爽'
            }
        },
        methods: {
            changes: function() {
                this.isHot = !this.isHot
            }
        },
        watch: {
            isHot: {
                immediate: true, //初始化时调用一下
                //监听值发生改变时，进行监测
                handler(newValue, oldValue) {
                    console.log('新值:' + newValue + '旧值：' + oldValue)

                }
            }
        },
    })

    //另一种写法
    v.$watch('isHot', {
        immediate: true, //初始化时调用一下
        //监听值发生改变时，进行监测
        handler(newValue, oldValue) {
            console.log('新值:' + newValue + '旧值：' + oldValue)

        }
    })
</script>
```

#### 深度监测

1. Vue中的watch**默认不检测对象内部值的改变(一层)**
2. 配置deep:true可以监测对象内部值改变(多层)
3. **Vue自身可以监测对象内部值的改变，但是Vue提供的watch默认不可以**
4. 使用watch时根据数据的具体结构，决定是否采用深度监测。

```js
//创建Vue实例
const v = new Vue({
    el: "#root",
    data: {
        stu: {
            liu: 1,
            yu: 2
        }
    },
    watch: {
        //监视多级结构某个属性的变化
        'stu.liu': {
            handler() {
                console.log('stu.lliu改变了')
            }
        },
        //监视多级结构所有个属性的变化
        stu: {
            deep: true,
            handler() {
                console.log('stu改变了')
            }
        }
    },
})
```

简写形式

简写就不能配置 imediate 和deep属性了

```js
==========原始形式============
    watch: {
        isHot: {
            immediate: true, //初始化时调用一下
                //监听值发生改变时，进行监测
                handler(newValue, oldValue) {
                console.log('新值:' + newValue + '旧值：' + oldValue)

            }
        },
    }

==========简写形式1============
    watch: {
        isHot(newValue, oldValue) {
            console.log('新值:' + newValue + '旧值：' + oldValue)
        }
    }


==========原始形式1============

    v.$watch('isHot', {
    immediate: true, //初始化时调用一下
    //监听值发生改变时，进行监测
    handler(newValue, oldValue) {
        console.log('新值:' + newValue + '旧值：' + oldValue)

    }
})
    ==========简写形式2============

    v.$watch('isHot', function(newValue, oldValue) {
    console.log('新值:' + newValue + '旧值：' + oldValue)

})
```

#### 计算与监视的对比

computed和watch之间的区别

- computed能完成的，watch也能完成
- **watch能完成的功能，computed不一定能完成。例如：watch内可以完成异步操作。**
- watch监听的属性需要提前data设置好，computed就不需要

注意：

- 所被vue管理的函数，最好写出普通函数，这样this的指向才是vm或者组件实例对象
- 所有不被vue管理的函数（定时器回调，ajax）最好写成箭头函数，这样this的指向才是vm或者组件实例对象

**computed不需要提前设置好属性**

```html
<div id="root">
    姓：<input v-model:value="firstName" />名：<input v-model:value="lastName" />
    <!-- 计算属性 -->
    <h1>{{fullName}}</h1>
</div>


<script type="text/javascript">
    Vue.config.productionTip = false

    //创建Vue实例
    const v = new Vue({
        el: "#root",
        data: {
            firstName: '刘',
            lastName: '强',
        },
        computed: {
            fullName: function() {
                return this.firstName + '-' + this.lastName
            }
        },
    })
```

**watch需要提前设置好属性**

```html
<div id="root">
    姓：<input v-model:value="firstName" />名：<input v-model:value="lastName" />
    <!-- 计算属性 -->
    <h1>{{fullName}}</h1>
</div>


<script type="text/javascript">
    Vue.config.productionTip = false

    //创建Vue实例
    const v = new Vue({
        el: "#root",
        data: {
            firstName: '刘',
            lastName: '强',
            fullName: '刘-强'
        },
        watch: {
            firstName(val) {
                this.fullName = val + '-' + this.lastName
            },
            lastName(val) {
                this.fullName = this.firstName + '-' + val
            }
        },
    })
</script>
```

### 1.8 class与样式

#### 绑定class

```html
<div id="root">
    <!-- 绑定class样式 字符串写法 适用于样式类名不确定，需要动态决定-->
    <div class="basic" :class="mood" @click="changeMood">{{name}}</div>
    <!-- 绑定class样式 数组写法 适用于要绑定得样式个数不确定，名字也不确定-->
    <div class="basic" :class="classArr">{{name}}</div>
    <!-- 绑定class样式 对象写法 适用于要绑定得样式个数确定，名字也确定 但动态决定用不用-->
    <div class="basic" :class="classObj">{{name}}</div>
</div>


<script type="text/javascript">
    Vue.config.productionTip = false

    //创建Vue实例
    const v = new Vue({
        el: "#root",
        data: {
            name: '刘强',
            mood: 'normal',
            classArr: ['atguigu1', 'atguigu2', 'atguigu3'],
            classObj: {
                atguigu1: true,
                atguigu2: false
            }
        },
        methods: {
            changeMood() {
                const arr = ['happy', 'sad', 'normal']
                this.mood = arr[Math.floor(Math.random() * 3)]
            }
        },
    })
</script>
```

#### 绑定style

```html
<body>
    <div id="root">
        <!-- 对象写法 -->
        <div class="basic" :style="styleObj">{{name}}</div>

        <!-- 对象数组写法 -->
        <div class="basic" :style="[styleObj1,styleObj2]">{{name}}</div>
    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false

    //创建Vue实例
    const v = new Vue({
        el: "#root",
        data: {
            name: '刘强',
            styleObj1: {
                fontSize: '40px',
                color: 'red'
            },
            styleObj2: {
                lineHeight: '20px'
            }
        },
    })
</script>

```

### 1.9 条件渲染

1. v-if

   ​	v-if="表达式"

   ​	v-else-if="表达式"

   ​	v-else

   ​	**切换频率较低的场景，不展示Dom元素直接移除**

2. v-show

   ​	v-show="表达式"

   ​	**切换频率较高的场景**

   ​	不展示Dom元素未被移除，仅仅只是样式隐藏		

3. 使用v-if时，元素可能无法获取，而使用v-show则一定可以获取到

```html
<div id="root">
    <!-- v-show做条件渲染 -->
    <div v-show="isShow">1{{name}}</div>
    <div v-show="1==1">2{{name}}</div>

    <!-- v-if做条件渲染 -->
    <div v-if="1!=1">3{{name}}</div>
    <div v-else-if="false">4{{name}}</div>
    <div v-else-if="true">5{{name}}</div>
    <div v-else>哈哈</div>

    <template v-if="true">
        <h1>template不会破坏页面结构</h1>
        <h1>v-if可以用于template v-show不可以</h1>
    </template>
</div>
```

### 1.10 列表渲染

```html
<div id="root">
    1.遍历数组 
    <ul>
        <li v-for="p in persons" :key="p.id">
            {{p.id}}-{{p.name}}
        </li>
    </ul>
    2.遍历对象 
    <ul>
        <!-- 值在前面,索引在后面 -->
        <li v-for="(value,key) in car" :index="key">
            {{key}}-{{value}}
        </li>
    </ul>
    3.遍历字符串
    <ul>
        <!-- 值在前面,索引在后面 -->
        <li v-for="(value,index) in str" :index="index">
            {{index}}-{{value}}
        </li>
    </ul>
    4.遍历指定次数 从1开始计数-
    <ul>
        <li v-for="(number,index) in 5" :index="index">
            {{index}}-{{number}}
        </li>
    </ul>
</div>

<script type="text/javascript">
    Vue.config.productionTip = false

    //创建Vue实例
    const v = new Vue({
        el: "#root",
        data: {
            persons: [{
                id: '001',
                name: '刘强',
                age: 24
            }, {
                id: '002',
                name: '俞文竹',
                age: 24
            }],
            car: {
                name: '雅阁',
                price: 200000,
                color: 'black'
            },
            str: 'hello'
        }
    })
</script>
```

#### key的原理

不设置id时，index作为key时

![1647056757518](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1647056757518.png)

不设置key作为id时

![1647056846993](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1647056846993.png)

vue中的key的作用

**虚拟Dom中的作用：**

key是虚拟Dom对象的标识，当数据发生变化时，vue会根据【新数据】生成【新的虚拟Dom】。随后Vue会进行新旧的差异对比。

**对比规则如下：**

- 旧虚拟Dom找到了与新Dom相同的key
  1. 若虚拟Dom中内容没变，直接使用之前的真实DOM
  2. 若虚拟Dom中内容变了，则生成新的真实Dom，随后替换掉页面之前的真实Dom
- 旧Dom中未找到与新Dom相同的key
  1. 创建新的真实Dom，随后渲染到页面

**用index做为key可能会引发的问题**

1. 若对数据进行：逆序添加、逆序删除等破坏顺序操作，会产生没有必要的真实Dom更新，界面效果没问题，但效率低。
2. 如果结构中包含输入类的Dom,会产生错误Dom更新。

**开发中如何选择key? :**

1. 最好使用每条数据的唯一标识作为key，比如id、手机号、身份证号、学号等唯一值。
2. 如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key是没有问题的。

#### 列表过滤

用计算属性实现

```html

<div id="root">
    <input type="text" v-model="keyWord" />
    <ul>
        <li v-for="p in filterPersons" :key="p.id ">
            {{p.id}}-{{p.name}}
        </li>
    </ul>
</div>

<script type="text/javascript">
    Vue.config.productionTip = false

    //创建Vue实例
    const v = new Vue({
        el: "#root",
        data: {
            keyWord: '',
            persons: [{
                id: '001',
                name: '刘强',
                age: 24
            }, {
                id: '002',
                name: '俞文竹',
                age: 24
            }, {
                id: '003',
                name: '吴云',
                age: 24
            }],
        },
        computed: {
            filterPersons() {
                return this.persons.filter(p => {
                    return p.name.indexOf(this.keyWord) != -1
                })
            }
        },
    })
</script>
```

用监视属性实现

```html
<div id="root">

        <input type="text" v-model="keyWord" />
        <ul>
            <li v-for="p in filterPersons" :key="p.id ">
                {{p.id}}-{{p.name}}
            </li>
        </ul>
    </div>

<script type="text/javascript">
    Vue.config.productionTip = false

    //创建Vue实例
    const v = new Vue({
        el: "#root",
        data: {
            keyWord: '',
            persons: [{
                id: '001',
                name: '刘强',
                age: 24
            }, {
                id: '002',
                name: '俞文竹',
                age: 24
            }, {
                id: '003',
                name: '吴云',
                age: 24
            }],
            filterPersons: []
        },
        watch: {
            keyWord: {
                immediate: true,
                handler(newValue) {
                    this.filterPersons = this.persons.filter(item => {
                        return item.name.indexOf(newValue) != -1
                    })
                }
            }
        },
    })
</script>
```

#### 列表排序

升序

```js
filterPersons() {
    const arr = this.persons.filter(p => {
        return p.name.indexOf(this.keyWord) != -1
    })
    return arr.sort((a, b) => {
        return a.age - b.age
    })
}
```

降序

```js
filterPersons() {
    const arr = this.persons.filter(p => {
        return p.name.indexOf(this.keyWord) != -1
    })
    return arr.sort((a, b) => {
        return b.age - a.age
    })
}
```

### 1.11 收集表单元素

```html

<div id="root">
    <form @submit.prevent="submit">
        
        账户<input type="text" id="accountID" v-model.trim="userinfo.accountID" /><br/> 
        密码<input type="password" id="accountpsw" v-model="userinfo.accountpsw" /<br/> 
        年龄<input type="number" v-model.number="userinfo.age" /><br/> 
 
        男<input type="radio" name="sex" value="male" v-model="userinfo.sex" /> 
        女<input type="radio" value="female" v-model="userinfo.sex" name="sex" /><br/> 
        
        爱好 
        学习<input type="checkbox" v-model="userinfo.hobby" value="study" /> 
        游戏<input type="checkbox" v-model="userinfo.hobby" value="game" />
        吃饭<input type="checkbox" value="eat" v-model="userinfo.hobby" /> <br/>
        
        所属校区
        <select v-model="userinfo.city">
            <option value=" ">请选择校区</option>
            <option value="beijing">北京</option>
            <option value="shanghai">上海</option>
            <option value="shenzhen">深圳</option>
        </select> <br/>
        
        其他信息
        <textarea cols="30" rows="10" v-model="userinfo.other"></textarea><br/>
        
        <input type="checkbox" v-model.lazy="userinfo.isread" />阅读并接受<a href="www.baidu.com ">《用户协议》</a>
        <br/>
        
        <button>提交</button>
        </form>
</div>


<script type="text/javascript ">
    Vue.config.productionTip = false

    //创建Vue实例
    const v = new Vue({
        el: "#root ",
        data: {
            userinfo: {
                accountID: '',
                accountpsw: '',
                sex: 'male',
                age: 23,
                hobby: [],
                city: '',
                other: '',
                isread: false
            }
        },
        methods: {
            submit() {
                console.log(JSON.stringify(this.userinfo))
            }
        },
    })
</script>

```

![1647265477889](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1647265477889.png)

### 1.12过滤器

过滤器：

定义：对要显示的数据进行特定格式化后再显式（适用于一些简单逻辑的处理）

语法：

**注册过滤器**：Vue.filter(name,callback)或 new Vue(filters:{})

**使用过滤器**：{{xxx|过滤器名}} 或v-bind:属性=”xxx|过滤器名“

注意：

1. 过滤器也可以接收额外参数，多个过滤器也可以串联
2. **并没有改变原本的数据**，是产生新的对应的数据

内部单个过滤器

```html
<div id="root">
    <h2>{{fmTime}}</h2>
    <!-- 过滤器实现  -->
    <h2>{{time|timeFormater}}</h2>
    <!-- 过滤器实现  传参-->
    <h2>{{time|timeFormater('YYYY年MM月DD日 HH')}}</h2>
    <!-- 多个过滤器实现 -->
    <h2>{{time|timeFormater()|silce}}</h2>
</div>

<script type="text/javascript ">
    Vue.config.productionTip = false

    const v = new Vue({
        el: "#root ",
        data: {
            time: 1647309962665
        },
        computed: {
            fmTime() {
                return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
            }
        },
        filters: {
            timeFormater(value, str = 'YYYY年MM月DD日') {
                if (str) {
                    return dayjs(value).format(str)
                }
                return dayjs(value).format('YYYY年MM月DD日 HH:mm:ss')
            },
            silce(value) {
                return value.slice(0, 4)
            }
        }

    })
</script>
```

组件全局过滤器

```html

<div id="root">
    <h2>{{fmTime}}</h2>
    <!-- 全局过滤器 -->
    <h2>{{time|mySlice}}</h2>
</div>

<script type="text/javascript ">
    Vue.config.productionTip = false
    // 全局过滤去
    Vue.filter('mySlice', value => {
        return dayjs(value).format('YYYY年MM月DD日 HH:mm:ss')
    })

    //创建Vue实例
    const v = new Vue({
        el: "#root ",
        data: {
            time: 1647309962665
        },
    })
</script>
```

### 1.13 内置指定

v-bind:单向绑定解析表达式,可简写为:xxx

v-model :双向数据绑定

v-for :遍历数组/对象/字符串

v-on:绑定事件监听,可简写为@

v-if:条件渲染（动态控制节点是否存存在)

v-else:条件渲染（动态控制节点是否存存在)

v-show:条件渲染（动态控制节点是否展示)

#### v-text

作用：向其所在的节点中渲染文本内容。不支持结构解析。

区别：**v-text会替换掉节点的内容**，{{xx}}则不会

```html
<div id="root">
    <h1>{{name}}</h1>
    <!-- 等同于 v-text-->
    <h1 v-text="name"></h1>
</div>
```

#### v-html

支持结构解析。

#### v-cloak

 **防止闪现, 与 css 配合: [v-cloak] { display: none }**

当资源加载缓慢时，页面可能出现未解析的html元素，当加载完才出现解析好的，这时候会出现闪烁抖动。所以需要可以加这个属性，然后给这个属性加样式。

资源加载完后，v-cloak属性移除

```html
<style>
    [v-cloak] {
        display: none;
    }
</style>


<div id="root">
    <h1 v-cloak>{{name}}</h1>
    <script src="http://127.0.0.1:5500/vue.base.js/js/vue.js"></script>
</div>


```

#### v-once

v-once所在节点在初次动态渲染后,就视为静态内容了。

以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。

#### v-pre

跳过所在节点的编译节点

可利用它跳过：**没有使用指令语法、没有插值语法的节点。会加快编译。**

### 1.14 自定义指令