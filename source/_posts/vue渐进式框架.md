---
title: vue渐进式框架
date: 2016-04-01 21:03:04
tags: 笔记
---

## Vue是什么?

>1. 构建用户界面的JavaScript`渐进式框架`
>2. 模仿angular框架开发的类似于angular
>3. 可以用来构建SPA应用程序(SPA single web application) `单页面应用程序,说白了就是页面不刷新`
>4. CDN: 加速 缓存技术
>5. Vue本身只是用于`数据驱动视图更新的一个库`

## Vue的特点

### MVVM

>`特点:数据驱动视图的方式`
>
>Model  数据
>
>View  视图
>
>ViewModel 数据驱动视图  数据一变化,视图也跟着变化
>
>面向数据式编程

### 组件化

>通过组件化开发极大的提高了开发的效率和可维护性

### Vue的优缺点

>1. 上手简单
>2. 简单的API
>3. 轻量高效
>4. 灵活的组件系统
>5. 强大的生态系统 :`Vue Router``Vues`等等一系列的系统
>6. 开源
>7. 号称屌丝福音

### 可以做什么

>1. 一切和web用户界面相关的都可以使用Vue来做
>2. 对SEO没要求的应用
>3. 更加侧重于单页面应用程序(SPA)开发
>4. 单产品型的应用程序
>5. 桌面应用程序 和其他技术相配合 纯Vue是写不出来的
>6. 管理系统
>7. 混合APP
>8. 移动APP

一些资源:官方资源 / 官方仓库/不要买书/分支主题

### Vue可以和jQuery库和其他类库使用

## 安装vue

>下包: npm i vue 
>
>在用Vue构建大型应用时推荐使用NPM安装
>
>Vue的核心只关注视图层 el部分就是视图层,视图层也叫模板层
>
>`data`叫数据或者模型

1. 第一步:npm i vue
2. 第二步:script标签引进来

```js
<script src='/vue.js'></script>
```

​	  3. 第三步:每一个Vue程序都是以 `new Vue()`开始的

```js
<div id='app'>
	<h1>{{ foo }}</h1>
</div>
<script>
	new Vue({
	el:'#app',
	data:{
	foo:'bar'
	}
	})
</script>
```

  4. 每一个Vue实例都是接收一个选项对象用来配置Vue应用

  5. 选项的`el`属性,用来告诉Vue的启动`入口节点`,凡是入口节点中的所有节点就可以使用Vue的语法了可以理解成`Vue是高级的模板引擎`

  6. Vue中的模板对象 `'{{ 插值表达式 }}'`数据是通过`data`选项来指定

     注意:el 不能挂载到HTML和body元素,只能是挂载一个普通元素,所有一般我们的页面一开始就来一个 div #app  el的值可以是CSS选择器,但是建议使用id选择器,如果选中了多个标签,那么只对第一个生效,,,el的值也可以是DOM节点,,例如:`el:document.querySelectorAll('div')[1];`这种方式很少用

## 初始Vue

Vue中的属性值如果是布尔值,一般如果不写的话,那么默认为true  

v-show:false  默认值为false

`<p v-show=''> hello world<p>`

>所有一般在工作中,我们不应该过度依赖默认值,使用属性时要给定值

想要将数据展示到标签内部我们可以使用`v-text`和 `{{ mag }}`这两种方式

>v-text 其实封装的是js中 innerText的属性 专门对文本进行绑定
>
>```html
><p v-text='msg'></p> 浏览器不闪,,因为这个v-text 是写在标签中的属性,所有浏览器不会闪
>```

><p id='pp'>{{ msg }}</p>  加载时浏览器会闪烁  因为浏览器是从上到下加载,先指向html标签中的内容, 在执行Vue中的逻辑代码,所以才会在加载时闪一下

```js
new Vue({
    el:'#app',
    data:{
        msg:'我是一个p标签'
    }
})
标签中的属性值是通过Vue对象中的data属性进行操作的
```

1. el只能挂载单一节点
2. `el data completed methods watch` 等等 这些都是实例选项,不同选项具有不同的作用
3. data中的数据不是普通数据,这种数据称之为响应式数据,用来驱动视图更新的数据

### data中数据类型初始化的几种方式

>数字: num : 0  数字的初始化为 0
>
>字符串: str : ' '  初始化为一个空字符串
>
>布尔值: isSeen:false  布尔值初始化为 false
>
>数组: arr[]   初始化为一个空数组
>
>对象: obj:{}  / obj:null  对象的初始化为一个空对象 或者是一个null

对于对象的修改:

1. 没有初始化的对象成员,如果修改, 不会更新视图
2. 可以动态添加未初始化的数据成员并且能够更新视图

```js
Vue.set(参数1,参数2,参数3)
参数1:app下的对象,例如:app.user
参数2: 需要添加属性名 如:'gender'
参数3: 新添加的属性名的属性值 '男'
```

1. 直接对对象践行重新赋值可以实现视图的更新  `app.obj={a:123}`
   * 对于对象中不存在的成员,浏览器不会报错,会是undefined,已经初始化的都可以正常更新,没有初始化的不能直接修改数据更新视图

## 数据绑定

什么是数据绑定:`模型中的数据与视图的对应关系就是数据绑定`

#### `v-bind` 专门对属性进行绑定

#### `v-text` 专门对文本进行绑定

Vue只关注`v-`开头的属性,不是以此开头的 默认是标签固有的标准属性,不归Vue管理

v-bind:title='title'    v-bind 是对属性的绑定

```js
<p v-bind:title='title'>{{ title }}</p>
new Vue({
    el:'#app',
    data:{
        title:'我是一只小青龙'
    }
})
```

F12中显示的是:<p title='我是一只小青龙'>我是一只小青龙</p>

>title 起到的作用是鼠标放上去显示对内容的解释

#### 	`v-bind:style={}` 这个数据绑定比较特殊,接收的是一个`对象类型`

```HTML
<p v-bind:style="{color:red,height:123px}">这是一种添加样式的方式</p>
```

我们一般使用以下方式添加样式

```js
<p v-bind:style="styleObject">这是另外一种添加样式的方式</p>
new Vue({
    //一定要写到data中,因为data是管理数据的
    data:{
        styleObject{  
        color:'red',
        background:'blue'
    }
    }
})
```

#### `v-bind:class `语法比较特殊,同样接收一个对象类型  对象属性为真实存在的类名,对象的值为布尔类型  如果为true则添加属性对应的类名..如果为false 则不添加属性 

```html
<style>
	.dome{
	color:red
	}
</style>
<p v-bind:class='{dome:false/true}'>这是一段带文字的段落</p>
// 简写 将v-bind省略掉
<p :class='{dome:false/true}'>这是一段带文字的段落</p>
```

>font-size, background-color这种有中横线的我们要写成 fontSize, backgroundColor

 样式也可以使用数组的形式书写,作为了解

```html
<style>
    .arr{
        color:blue;
    }
    .err{
        font-size:50px;
    }
</style>
<div :class='[arroy,error]'>下个路口见</div>
data:{
	arroy:'arr',
	error:'err'
}

```

>总结:
>
>`:class`
>
>`:style`
>
>这两个属性后面接收的都是一个`对象类型` : 冒号是v-bind的简写

```js
p{{list[0]}}p

data:{
	list:['html','css','js']
}
// 输出 html

<p>{{user.name}}{{user.age}}<p> 或者 <p>{{user['my-sex']}}</p>
data:{
    user:{
        name:'小明',
        age:18,
        my-sex:'男'
    }
}
```

>在浏览器控制台中可以获取到data中数据
>
>vm.name 或 vm.$data.name

## 事件绑定

### 语法: v-on:click='回调函数'

v-on:click/ change /blur /focus /submit(一般用于form表单提交 回车可直接提交)

```js
new Vue({
    //Vue提供的专门定义方法的参数 methods
    //也可以定义事件函数的回调
    methods:{
        clicked:function(){
        }, //---方法与方法之间用 ','隔开
        onchange(){
        }
    }
})
```

### v-on 可以删掉用@ 符号代替

>@事件名称='回调函数'
>
>//回调函数写到methods 里面,,,里面还是可以传参数的,js中参数怎样传,这里面就怎样传
>
>```js
><input type='text' @focus='fac'@blur='blu'/>
>
>methods:{
>   fac(){
>       console.log('获取鼠标焦点')
>   },
>   blu(me){
>       console.log(me,'失去光标焦点')
>   }
>}
>```
>
>

当事件被触发时,可以将事件对象以参数形式传递,,`$event` 在vue中是具有特殊函数的内容,,在这里表示`事件对象`

```js
<input type='text' @focus='fac($event)'/>
<div id='app'>
  <input type='text' @focus='onclick(a,$event)'>
  <a href='#'@click='clicks(b,$event)'>点我</a>
</div>

new Vue({
    el:'#app',
    data:{
        a=10,
        b=20
    },
    methods:{
        onclick(a,e){
            console.log('我是一只小青龙')
            console.log(a,e)
        },
        clicks(b,e){
            console.log('我被点击了')
            console.log(b,e)
            //超链接点击之后,改变当前被点击的DOM节点的颜色
           	e.target.style.background='blue';
            e.target.style.color='yellow';
        }
        
    }
})
```

### vue中的修饰符

1. 在Vue中通过修饰符来解决事件执行时的一些特殊逻辑问题,如 阻止冒泡` @事件名.stop='函数'`

2. 如:获取按键信息,这些都是可以通过事件修饰符来获取

`@keyup.13='send'`/ `@keyup.shift.enter='send'`

3. 阻止按钮默认行为

   `@submit.prevent='函数'`

   以下几点:都会触发表达提交行为:点击type='submit'的input 点击表单中的普通按钮,在文本框中敲回车 更建议的是使用form的submit事件来注册表单提交处理函数 

   例如:阻止了按钮的默认行为,将事件注册给form标签中

   ```html
   <form @submit.prevent='onSubmit></form>
   ```

4. 按键修饰符:

   >@keydown.enter 回车
   >
   >.tab tab键
   >
   >.delete 删除键
   >
   >.esc 取消键
   >
   >.meta  windows
   >
   >.....

在Vue中, 有且只有V-bind 和 v-on 有简写,,其他的属性 都没有简写 ` v-bind =>  :` `  v-on => @`

`var vm=new Vue({})  事件处理函数中的this指向的是 Vue的实例对象,也就是vm`

注意:事件处理函数 不能使用箭头函数定义,因为methods中的this指向的是window

当处理函数的代码只有一句的时候,我们可以直接写到模板中:注意这里不需要加this

```js
<h1>{{ message }}</h1>
<button @click='message='hello'>测试</button>
//如果想改变h1中的内容时,我们就直接在button中写逻辑即可
```

属性格式:

```html
<li v-for='(item,index) in items'>{{ item.name }}</li>
```

## 响应式的数据绑定

实例化对象 可以直接访问模型中的数据

```js
var vm=new Vue({
    data:{
        msg:'数据初始化',
    }
})
console.log(vm.msg)
```

> `**methods:中的this指向的是Vue实例(实例对象)**`
>
> 实例对象vm 不但可以直接访问模型(data)中的数据,还可以访问methods中的方法
>
> 注意:以下两种情况都不会更新视图
>
> 1. 当你利用索引值直接设置一个数组项时,不会更新视图  例如: vm.items[index]=newValue;
>
>    ```js
>    //错误
>    var vm = new Vue({
>          var arry = [1,2,3];
>        })
>        vm.arr[0] = 4;
>    
>    //正确
>    Vue.set(arr,0,4)
>    解决方案:Vue.set(参数一,参数二,参数三)
>    参数一:实例数组
>    参数二:索引值
>    参数三:你要修改的下标的值
>    ```
>
>    2. 当你修改数组长度的时候,也不会更新视图------>了解即可

## 双向数据绑定(重要)

```js
<input type='text' v-model='text'>
v-model 就能获取到用户输入的信息
<div id='app'>
    <input type='text' v-model='text'>
    <h1>{{ text }}</h1>
</div>

var vm=new Vue({
    el:'#app',
    data:{
        text:'',
    }
})
```

`data中定义了属性,methods中就不能定义与data中的属性相同的名称`

methods中定义的方法不允许使用箭头函数

>`v-model是将视图的数据流向模型`
>
>`v-text v-html是将模型中的 数据流向视图`

```js
 <div id="app">
    <!-- 双向绑定的思路： 1.获取到输入框中的内容2.将获取到的内容设置到h1标签中-->
    <input type="text" v-model="msg">
        //h1里面绑定的是data中的msg,数据流向视图
        //input里面用了v-model这个属性,v-model绑定的是data里面的msg 所有input输入框里面的值改变,data里面的msg就变,h1 里面的{{msg}}也跟着变
    <h1 :style="styleObject">{{msg}}</h1>
  </div>

new Vue({
    el: '#app',
    data: {
      msg: '',
      suiji: Math.random() * 255,
      styleObject: {
        color: 'rgba(this.suiji,this.suiji,this.suiji)',
        background: 'blue',
        fontSize: '36px',
      }
    },
    methods: {

    }
  });
```

**v-model 如果作用到输入框中时,在Vue底层中其实就是在监听input事件**

## 条件渲染 结构

v-if是根据绑定数据的真假来决定是否渲染(在视图中展示)这个元素  v-if是真正的条件渲染

v-if -->v-else-if  --->v-else 

v-if和v-else 之间不能出现其他标签,否则会报错儿  这个其他标签指的是不带v-if/v-else的标签,如果v-if和v-else之间出现了其他的v-if/v-else标签,浏览器是可以解析的

```js
<p v-if='age<18'>我小于18</p>
<p v-else-if='age>18'>我大于18岁</p>
<p v-else>我等于18岁</p>  ----->最后这个v-else不需要再写值了
```

```js
//错误示范
<p v-if='1===1'>hello</p>
<p>hello</p>
<p>world</p>

//正确示范
<p v-if='seen'>hello</p>
<p v-if='1===1'>hhaha </p>
<p v-else>456</p>
<p>world</p>
```

> v-show 我们叫条件显示  工作中使用v-show而不使用v-if
>
> 如果使用频率一直是显示隐藏,`频率较高`,那么我们就使用`v-show`   这个方法是在标签中加了属性 display=none  所有节点还是在的
>
> 如果将dom节点删掉再也不出现,那么我们就是用v-if

v-show不能结合v-else使用,,,v-if只能和v-else结合使用

### v-if和v-show的区别

1. v-if条件渲染,如果条件为false 则不渲染元素
   * true 渲染DOM
   * false 不渲染 DOM
2. v-show条件显示,无论条件的真假使用都渲染元素
   * true 渲染DOM
   * false渲染DOM ,不显示(display:none)
     * 不能和v-else v-else-if结合使用

### 遍历数组

```html
v-for='item in items'
<li v-for='item in items'>{{ item }}</li>
<li v-for='(item,name,index) in items'>{{index}}-{{item}}</li>
这里的name表示的是对象的键名
```

## input事件

>只要一输入内容的时候就触发了这个事件,输入内容的过程中就是一直在触发这个事件

## 关键字

暂时遇到的不能用的关键词 :`in` `delete` `header`

## key的使用(重要)

### 什么是key

> 1. key是vue提供的一个特殊属性
> 2. key的数据类型必须是数字或者字符串
> 3. key的值不能是数组或对象或者布尔值

**Vue中在进行模板渲染时,为了提升性能,它并不是每次都有创建成新的节点,它会复用已经创建的DOM节点**

**key是用来区分标签名一样的dom节点 相当于id**

通过key属性可以强制告诉vue 重新创建生成一个DOM节点

v-for都要加上key,但是key的值不能是数组中的索引值,我们一般使用id值 `key是唯一的值`

`v-for是否重新渲染取决于key的值是否是变动的,如果是不变的,那么就不重新渲染,,如果key的值也是变的,那么就需要重新渲染`

## template

`当需要遍历多个元素而又不想添加额外的元素节点时 我们就使用template`

注意:

1. template中不能添加key 需要将key添加到真实的DOM节点上...
2. template是Vue中特殊提供的一个元素,浏览器并不会解析,因为它不生成标签
3. 在template中使用v-show是无效的,只能是使用v-if

## 表单输入绑定

`v-model`**最常用的需求就是提交表单**

问题:如何获取表单数据

v-model文本框: 

	1. 它会把数据绑定到input的value属性中

   	2. 当input中输入改变的时候,它会自动把数据重新赋值给data中的响应参数

## 绑定复选框

复选框一般是绑定一个布尔值来决定是否选中,true为选中,false为没选中

```
<input type='checkbox' v-model='check'>
data:{
	check:true
}
```

## 绑定单选框

单选按钮,它会把value===数据的radio设置为被选中状态

试图改变的时候,它会把用户选中的radio的value同步到data中的数据中

```js
<input type='radio' name='gender' value='男' v-model='gender'>男
<input type='radio' name='gender' value='女' v-model='gender'>女
data:{
    gender:'男';
}
```

## 选择下拉框数据绑定

1. 数据更新视图,它会找到option中的value=city元素项,设置选中状态
2. 视图更新数据,他会把选中的那个option的value同步到数据中

```js
<select v-model='city'>
    <option value='上海'>上海</option>
	<option value='北京'>北京</option>
	<option value='广州'>广州</option>
	<option value='深圳'>深圳</option>
</select>
 data:{
     city:'上海'
 }
```

# day2

## 指令

指令是带有v-开头前缀的特殊特性,这里的特性就是属性

`mounted:在这发起后端请求,拿回参数`,配合路由钩子做一些事情(dom渲染完成 组件挂载完成)

`v-once ` 只执行一次   <p v-once>{{ text }}</p>

`v-cloak` :组织闪烁

```html
style 标签中需要写:
<style> 
<--使用属性选择器-->
    [v-clock]{  display:none;}
</style>
一般我们就是将这个v-clock放到 #app的div中
<div v-clock id='app>
    <h1>{{ msg }}</h1>  --->这里所说的闪烁其实就是说的在页面加载的时候标签中的内容{{ msg }}在页面上不闪烁,这里的不闪烁并不是不刷新的意思
</div>
```

`v-pre`这个指令表示的意思是, 标签加了这个属性之后,表示该标签就不会被Vue程序进行解析了

### `v-model`**非常重要的指令**

常用的三个修饰符

.lazy     

.number      转数字格式

.trim     清除两端空格

`v-model.lazy`--->监听的是change事件,内容改变的时候,触发change事件,加上了 .lazy某种程度上可以提升性能

```html
<h1>{{ username }}</h1>
<input v-model.lazy='username'></input>
data:{
	username:'',
}
```

当文本输入框失去焦点的时候,就触发了 .lazy事件,,将 v-model获取到的文本输入框中的内容添加到h1标签中,但是前提是模型中要有一个username这个数据

`v-model.number` 将字符串的数字转成number类型

`v-model.trim` 清除两端的空格

<input type='password' v-model.trim='pwd'>

如果是多选框,数据类型将定义为`数组`

下拉框中的option的value属性不建议省略

```html
<select>
    <option value=''>请选择</option>
    <option value='1'>北京市</option>
    <option value='2'>天津市</option>
    <option value='3'>上海市</option>
</select>
如果不指定value值,那么就以文本内容为参照
如果制定了value值,那么就以value值为参照
```

### 指令动态参数

```js
<img v-bind:[aaa]='这是一张图片'>
<p v-bind:[aaa]='msg'>学习:Vue</p>
data:{
    aaa:'title',
    msg:'学习Vue.js'
}
```

如果属性绑定的值为一个动态(即一个变量)

那么这个变量就用中括号来包裹`[]`

<input @[myevent]='函数' type='text'>

data:{

​	myevent:'input'

}             ------>事件名也可以做成变量

## 计算属性

> computed中的数据是动态的,data中的属性是静态的

如果页面中的数据有不确定,我们可以使用计算属性来做

计算属性是只计算一次,然后把结果缓存起来,使用的时候直接使用缓存的数据即可

> 计算属性特点:
>
> 计算属性会把执行之后的结果缓存起来,多次使用结果的时候,就直接从缓存中获取即可
>
> 注意:计算属性不是方法,更不能当做事件处理函数使用,只要是事件处理函数的逻辑,肯定是在methods中调用函数,`计算属性一定要有返回值`, 返回值就是属性的值, 它的值可以在函数中通过更多的自定义的代码逻辑来实现
>
> `计算属性本质就是方法,但是只能是当做属性来访问,不能当做方法来调用`

计算属性的选项,和data methods平级

```js
computed:{
    //从字面上理解,所谓的计算属性是要经过计算才能得到的值 该函数的返回值即为计算属性的值
    students(){
        
    }
}
```

一个函数的返回值当做一个变量

`计算属性自带缓存机制,计算属性一定要有返回值`

初始化对象的时候我们使用null来初始化

## 倾听器 watch :{ }

```js
和data平级的
data:{}
watch:{} -->倾听器
computed:{} -->计算属性
methods:{}--->函数
```

```js
watch:{
	对data中的msg进行侦听
	属性名:要监视的数据成员
    属性值是一个处理函数
    Vue会将数据改变的新值和旧值作为参数传递给处理参数
    作用:当被监视的数据发生变化的时候,它会自动调用处理函数
    注意:他不需要返回值,更不需要在模板中绑定的.
    这里的msg是data选项中的数据成员
    watch中的成员不是数据,不是用于模板绑定的,watch是一个功能特点
    msg:function(newData, oldData){   
    }
}
```

当需要根据数据变化执行一些特定业务逻辑的时候,可以使用watch监视来实现

```js
watch:{
    //watch中每当被监视的数据发生改变的时候,就会触发watch中的逻辑代码
    如果被监视的数据类型是数组的话,那么watch默认的是只监视数组中的元素的个数增加了或者减少了,如果数组中的元素内容改变了,watch默认是见识不到的,所有 这里 例如 arr是个数组,逻辑是每当arr数组中添加了元素或者删除了元素(可以这么理解,watch默认只要是arr数组中的元素个数发生了改变,就会触发watch中的逻辑代码)就将数组arr的数据存放到本地
    arr:{
        handler(){  --->handler(){}这是固定格式
            window.localStorage.setltem('token');
        }


//如果需要watch监视每个元素中的内容是否发生了改变,其实也就是需要让watch进行深度监视,不光让watch监视数组的长度,还要watch监视元素的内容是否发生了改变,我们将这种监视成为深度监视,我们使用deep,默认deep是false,如果想要watch进行数组的深度监视,需要将deep的值改为true即可,,deep适合handler同级的
        deep:true
    }
}
```

## 过渡&动画

## 实例属性

### v-model用于多个复选框的使用

实践建议:所有的事件名称建议都起名为 onXXX例如: onAdd onDel 等等

`e.target.checked 触发该事件的DOM元素,原生的checkBox有一个属性checked可以获取选中状态`

### todosMVC项目步骤

1. #使用Git把模板下载到本地
2. $git clone (克隆代码链接)
3. 切换到todomvc-vue 目录中,安装依赖项
4. cd下载的项目中

#模板项目把样式等文件放到了第三放包里面了,所以我们要执行 `npm install`安装它的那些依赖项才能正常的预览到这个项目里面

`npm install`---> 下载依赖

`npm i vue`

# day03

>无论通过什么方式来获取checkbox改变之后的状态,都建议使用`change事件`,不要使用click点击事件,因为点击事件触发的时候,checkbox的状态可能还没有改变呢,通过事件对象来获取选中状态: 
>`e.target.checked`
>如果只是单纯的需要获取元素的选中状态,那么通过DOM获取就足够了
>如果期望checkbox受Vue动态影响,那就要给它进行数据绑定

## 和服务端通信

> axios也不操作DOM 也不操作视图,,这个第三方库就是用来接收发送请求的

### JSON-server工具的使用

> JSONServer 是一个提供测试环境接口的工具,它可以帮我们快速生成一套接口服务,专门用来学习测试

1. 安装JSONserver

   `npm install -g json-server`

2. 创建一个名叫json-server的文件夹,文件夹中创建一个文件叫 db.json 在这个文件中写出一下内容

```js
{
    "posts":[
        {"id":1,"title":"json-server","author":"typicode"}
    ]
}
```

3. 开启服务

在json-server目录下执行以下命令

`json-server--watch db.json`

如果看到一下信息,说明开启了服务

### 按照这套服务的接口文档

业务    请求方式   请求地址

增     POST          http://localhost:3000/users

删     DELETE http://localhost:3000/users/1 -->id

改     PATCH   http://localhost:3000/users/2 -->id

查     GET    http://localhost:3000/users

只有当删和改的时候需要在请求地址中传id,增和

### axios第三方库的使用

先下载`npm install axios`

增: POST请求

删: DELETE

改: PATCH

获取指定条件的数据

代码实现指定条件查询数据

`get参数往params中放`

`post参数往data中放`

#### 配置axios参数

配置请求道基地址

```js
axios.defaults.baseURL='http://localhost:3000/'
axios({
    method:'GET',
    url:'/user'
}).then(res=>{
    console.log(res)
}).catch(err=>{
    console.log(err,'获取数据失败')
})
```

`在axios中默认只有>=200和<400 的状态码都认为是成功的`

请求失败执行catch中的代码,请求成功之后执行then中的代码

catch捕获到的错误:

请求失败了!Error:Request failed with status code 404

#### Vue中获取表单数据的方式:

视图:我们对每个表单元素都设置v-model属性

模型:在模型中根据接口和视图抽象出来数据初始化到data中

建议表单相关的数据放到一个单独的数据对象中

```js
data:{
    user:{
        name:'',
        age:'',
        gender:''
    }
}
```

## created实例选项

补充一个Vue的实例选项 created和data平级,`created就是一个函数,这个函数在页面加载完毕之后就执行`,我们可以在created中访问this获取Vue实例

我们不太建议在created中写大量的业务逻辑代码,我们更推荐把这些功能都封装成一个函数放到methods中

### axios也是异步请求

# day 04

## 组件基础学习

> 场景:
>
> 重复的结构,重复的逻辑,重复的变量,我们就可以抽取成一个组件

给全局 Vue对象注册一个组件 component() 中 有两个参数,第一个参数是组件名

Vue.component('组件名',{组件对象})

### template中的DOM有且只有一个根节点

全局注册组件:全局实例共享组件

Vue全局对象 `Vue.component()`在Vue全局对象上注册一个全局组件

new Vue(el:'app')

所有的Vue实例就都可以使用这个全局组件

局部注册组件:只有在当前实例可以使用组件

组件的特点:

1. 如果是全局组件 应该写在实例化之前

2. Vue.component(组件名,组件对象);

   组件名的规范:'abc单词模式/abc-d双词模式 全部小写

   例如:Vue.component(`'eight-eight'`,{

   //组件对象

   //template中的模板中一定要注意,模板中有且只有一个根节点/根元素  template代表页面结构

   })

3. 组件是一个特殊的Vue实例

局部组件:需要在当前实例上注册

var vm= new Vue({

​	component:{

​		key:value形式

​		key表示是组件名 value表示的是组件对象

​		'abc-d':{

​			template:`<p>我最厉害</p>`

​	}

}

})

### 全局组件和局部组件的区别

注册位置不同,应用范围不同,全局的作用域范围更大

### 组件的嵌套

组件嵌套 就是在组建中使用其他最贱

### 组建通信

`父--->子  (重要) 给谁传就在水的标签上写属性,属性名随便写`

使用props是和template同级的,用来接收父传过来的数据

props:['属性名']--->字符串的数组

## 单页面应用--SPA

spa缺点:

1. 首屏加载慢,按需求加载,不刷新页面,只请求js模块
2. 不利于SEO-->服务器渲染
3. 开发难度高(框架)有一些学习成本和应用成本

### SPA实现原理

Vue-router需要下载

`组件:一个.vue文件就是一个组件`

`路由:地址发生改变,切换组件,但是页面不进行刷新`

## vue-router动态路由

引入vue-router的js文件

定义导航 <router-link></router-link>

定义容器 <router-view></router-view>

实例化vue-router

```js
var router=new VueRouter({
	routes:[
	//动态路由传参
	//定义动态路由参数
{
	path:'/company/:companyname',
component:{
	template:`<div>我从黑马毕业之后想去:</div>`
     }
   }
  ]
})
```



$route.params.companyname

`解释:$router.params可以获取到所有动态数据传过来的集合`

### vue-router to的属性赋值

## vue-router的重定向

>拦截谁就在谁的路由上写redirect
>
>redirect:'/beijing'

## vue-router编程式导航

>导航可以不要,容器必须要
>
><router-view></router-view>必须要
>
>push是替换一条数据,使用replace自始至终都只有一个数据
>
>go 是前进或后退一条记录 go(-1/1)

```js
methods:{
    gochaoyang(){
        //使用replace的时候是将地址进行了替换,始终保存的是一个地址
        //this.$router.replace('/chaoyang');
        this.$router.push('/chaoyang')
       	//this.$router.go(1)
    }
}
```

## 激活路由样式

```html
<style>
    .router-link-active{
        font-size:50px
        color:aqua;
    }
</style>
```

>直接就在style标签中写 .router-link-active这个类名就可以啦

## 嵌套路由

二级导航的导航和容器要在一级的组件中配置

还有children 选项,这个选项中写二级导航的路由表

# day05

## vue-cli 工具(脚手架)

### 安装

`npm i -g @vue/cli`

查看版本: vue-V(大V)  或者 vue-version

安装桥接工具将2.0的功能补齐到4.0的脚手架上

`npm install -g @vue/cli-init`

//卸载包

`npm uninstall  @vue/cli-init`

解决下载包不成功的问题,因为npm的服务器在国外在 百度中输入 cnpm

点击淘宝镜像

复制 npm install -g  cnpm --registry=http://registry.npm.taobao.org  回车执行以后下包的时候直接写cnpm即可

`cnpm i-g @vue/cli`

## 使用vue-cli创建项目

vue init webpack-simple heroes

heroes 是一个项目名,自定义的名

>#heroes  创建的项目名称
>
>$vue init webpack-simple heroes // webpack-simple 为模板名称 固定写法
>
>#切换到当前目录
>
>$cd heroes
>
>#安装依赖
>
>$cnpm install
>
>#在开发模式下,  启动运行项目
>
>$ npm run dev
>
>如果浏览器没有自动打开,也可以手动打开浏览器,在地址栏写: http://localhost:8080/ 回车即可

创建项目:采用cli 2.0 的特性(生成建议模板)

在heroes文件夹下打开powershell命令工具

安装一个bootstrap的固定版本 这是一个运行时依赖

`npm ibootstrap@3.3.7`

安装完毕后需要看一下dependencies 中有没有'bootstrap':'3.3.7' 如果有的话,就说明安装成功了

> 运行时依赖
>
> npm i 包名 -s或者 --save是安装运行时依赖  -S和 --save在npm中是可以省略的,但是在 cnpm中是不可以省略的 cnpm i 包名 -S 或者 --save

> 开发时依赖
>
> npm i 包名 -D 或者 --save --dev 是安装开发时依赖

安装完成bootstrap之后,在main.js入口处引入css文件

//在main.js中引入bootstrap的css文件和index.css文件

import from '../node_modeles/bootstrap/dist/css/bootstrap.css'

import from './style/index.css'

这个index.css样式在模板的静态页面中的css文件夹中放着,style文件夹是在src文件夹下新建的文件夹,专门用来放我们的样式文件

安装了bootstrap后会报错儿需要配置一下

```js
{
    test:/.(ttf|woff2|woff|eot)$/
    loader:'file-loader'
    options:{
        name:'[name].[ext]?[hash]'
    }
}
```

