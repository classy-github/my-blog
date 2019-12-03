---
title: jQuery-第三方类库
date: 2016-03-12 21:46:04
tags: 笔记
---
# Day1

## 1.什么是jQuery?

* j          ----> javaScript
* Query ----> 查询
* 也是一种js库  本质 还是js代码

## 2.其他方面理解jQuery

* jQuery:是一种js库

* 本质:将我们之前所学的js中用来操作页面中元素的,属性,方法,事件,动画................封装成了一个js文件(js库)

## 2.jQuery的优点?

* 让代码更高效
* 链式编程
* 隐式迭代(遍历元素)

## 3.jQuery中的顶级对象是谁: $

## 4.掌握通过jQuery的方式操作页面中的元素(1.选中标签,,2, 设置样式)  (重点)

1.先要引入jQuery文件 (js文件)

* 下载文件 （https://jquery.com/）
  * production jQuery  3.4.1 压缩后的一个js文件
  * development  jQuery  3.4.1 没有压缩的js文件
* jQuery 其他版本地址: （https://code.jquery.com）

2.在网页中引入对应的jQuery文件

* 如果用原生的js操作页面中的元素,假如将原生的js写到页面中 元素的前面,不能操作页面中的元素.假如需要操作,那么需要写   window.onload=function(){}

* 如果要使用jQuery操作页面中的元素,假如将jQuery代码放到了元素的前面,不能操作页面中的元素.如果要操作页面中的元素 有两中写法:

  * $(document).ready(function(){});

    或者

    $(function(){});

3.$  介绍

* $ 其实就是jQuery的别名
* $ 是jQuery中的顶级对象

4.dom对象和jQuery对象相互转化

* 1.如果我们通过jQuery方式获取到的元素,那么得到就是一个jQ对象,是以伪数组的形式保存的对象.
* 2.如果我们通过原生js的方式获取到的元素,那么得到的是一个dom对象
* 3.总结:
  * jQ对象只能使用jQuery中的属性和方法
  * DOM对象只能使用dom中的属性和方法
  * 如果想要jQ对象使用dom中的属性和方法,那么需要将jQ对象转化为dom对象
* 4.将jQ对象转化为DOM对象的方式:
  * jQ对象[0]   ---->转换成了的dom对象
  * jQ对象.get(索引)  ----> 转化为dom对象

```js
//1.获取到div
var div= $('div');
//2.将jQ对象转化为dom对象
div[0]
//3.将jQ对象转化成dom对象
div.get(0)
```

* 5.将DOM对象转化为jQ对象
  * $(dom对象)  ----->转化为jQ对象

```js
//1.使用原生的js方式隐藏div
var div=document.querySelector('div');
//2.使用原生的dom将元素隐藏
div.style.display:'none';
div.hide();
//3.将dom对象转化为jQ对象
$(div).hide()

//=======jQ版本
$(function(){
    //1.获取到div
    var div= $('div');
    div.style.display:'none';
    //2.将jQ对象转化为dom对象
    div[0].style.display:'none';
    //3.将jQ对象转化为dom对象
    div.get(0).style.display='none';
    //打印div
    console.dir(div)
    
})
```



5.jQuery中获取元素的方式

* 获取页面的元素

* $('css选择器')

  * css选择器
    * 标签选择器,类选择器,ID选择器,后代选择器,子代选择器,结构伪类选择器

* jQ中使用自己的方法选中页面中的标签

  * **jQ对象.parent()  ---->获取直接父元素**
  * **jQ对象.parents() ---->获取所有父辈元素**
  * **jQ对象.children(['选择器'])  ----->获取当前元素中的所有直接子元素(类似于css中的子代选择器)**
  * **jQ对象.find(['选择器']) ----> 获取当前元素中的子元素,子元素中包括了直接子元素和间接子元素(类似于css中的后代选择器)**
  * **jQ对象.siblings(['选择器'])  ---->获取当前元素的所有兄弟元素**
  * **jQ对象.hasClass('类名')  ---->获取当前元素是否有某个类名,返回布尔类型的结构**
  * **jQ对象.eq(index)  ----> 获取指定索引的标签(元素)**

* 注意:

  * 1.选择器中必须使用  引导
  * 2.jQ对象.parents('选择器')  ----->获取所有父辈元素中的指定的父元素

```js
<div class="box">
    <div class="nav">
      <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
      </ul>
    </div>
    hello
  </div>

console.log($('.nav').parent());
    //输出 div.box
    console.log($('li').parents());
    //输出 ul div.nav div.box body html
    console.log($('ul').children());
    //输出5个li
    console.log($('ul').children('li:nth(3)'));
    //输出下标3
    console.log($('.box').find('li'));
    //输出5个li 注意 想要拿到哪个标签 要在find里面写上
    console.log($('li').siblings());
    //输出5个li
    console.log($('.box').hasClass('.nav'));
    //输出false
    console.log($('li').eq(1));
    //输出下标1
```



6.jQuery 中操作元素样式

* 语法:
* 1.**jQ对象.css('属性' ,'值')   | jQ对象.css({属性:值 , 属性:值})**

```js
$('.box').css('background','red');

$('.box').css({
    background: 'red',
    color: 'blue'
  })
```

* 2.可以动态的给标签添加样式 实现样式的操作

  * jQ对象.addClass('类名')  ------>添加样式 类似于 classList.add()
  * jQ对象.removeClass()  ---->移除所有的类名
  * jQ对象.removeClass('类名') ----> 移除指定类名
  * jQ对象.toggleClass('类名')  ----->切换类样式(如果有,那么删除,如果没有该样式,就添加)

* 注意:

  * 1.如果通过addclass()给元素添加多个类名,那么类名中间使用空格 隔开.

    $('div').addclass('.box test');

  * jQ对象.addclass().addclass(),添加多个类名

```js
 $(function() {

    //添加类名 两种方式
    $('.box').addClass('name test');  
     //输出:<div class="box name test"></div>
     
    $('.box').addClass('item').addClass('text')
     //输出<div class="box name test item text"></div>
     
      //移除所有的类名
      // $('.box').removeClass();
     //输出<div class=""></div> 
     
      //移除指定了类名
    $('.box').removeClass('name');
     //输出:<div class="box test item text"></div>
     
    //切换类名,有移除,无则添加
    $('.box').toggleClass('item name');
     //输出:<div class="box test text name"></div>
  })
```

隐式迭代: jQ自己内部就可以将数组进行遍历,不需要我们手动遍历

注意: 

* 1.阻止a标签跳转页面:

```js
<a href="javascript:;"></a>
```

* 2.另外一种写法:

```js
a.onclick=function(){
    return false;
}
```

* 3.onmouseenter鼠标进入事件

* 4.onmouseleaves鼠标离开事件

* 5.通过jQ获取标签的索引值

  ​	**jQ对象.index()**

  

7.jQ中动画效果

* 1.元素的隐藏和显示

  * hide(参数1,参数2,参数3):
    * 参数1:动画的速度类型('slow','normal',fast, | 设置一个毫秒数)
    * 参数2: 动画切换效果('linear','swing')
    * 参数3:动画完成后的一个回调函数
  * show():参数与hide() 方法中的参数一样

* 2.滑动效果

  * slideUp(参数1,参数2,参数3):
    * 参数1:动画的速度类型('slow','normal',fast,  | 设置一个毫秒数)
    * 参数2: 动画切换效果('linear','swing')
    * 参数3:动画完成后的一个回调函数
    * 注意:
      * 1.slideUp()也可以隐藏元素,通过改变元素的高度(向上拉)
      * 2.slideDown()显示元素,通过改变元素的高度(向下拉)

* 3.淡入淡出效果

  * fadeIn(参数1,参数2,参数3):
    * 参数1:动画的速度类型('slow','normal',fast,  | 设置一个毫秒数)
    * 参数2: 动画切换效果('linear','swing')
    * 参数3:动画完成后的一个回调函数
  * fadeOut(参数1,参数2,参数3)
    * 参数1:动画的速度类型('slow','normal',fast,  | 设置一个毫秒数)
    * 参数2: 动画切换效果('linear','swing')
    * 参数3:动画完成后的一个回调函数
  * 注意:
    * 1.fadeIn()通过控制元素的透明度实现显示元素
    * 2.fadeOut()通过控制元素的透明度隐藏元素
  * fadeTo(参数1,参数2(必填),参数3,参数4)
    * 第一个参数:代表动画的速度
    * 第二个参数:代表透明度,必须设置,取值0-1之间
    * 第三个参数,动画切换的效果
    * 第四个参数,代表回调函数

  *4.自定义动画

* 语法:

  * jQ对象.animate({属性:值, 属性:值})

  注意:

  * 1.animate中不能设置与颜色相关的动画效果

DOM 学到的

属性  方法  事件 动画.



1.引入jQuery文件

2.

$("div").hide(); 隐藏div

ready 准备  find 找

首先先引入jq文件,在在script里面编辑

$ 是jq里面的顶级对象

window是js中的顶级对象

console.dir  以对象的方式将元素输出

对象里面有键值对

dom对象和jQ对象相互转化

* 如果我们通过jQ方式获取到元素,那么得到的就是一个jQ对象,是以伪数组是的形式保存的对象

* 如果我们通过原生js的方式获取到元素,那么得到的是一个dom对象

  * 总结:
  * jQ对象只能使用jQ中的属性和方法
  * DOM对象只能使用dom中的属性和方法
  * 如果想要jQ对象 使用dom中的属性和方法,那么需要将jQ对象转化为dom对象

* 将jQ对象转化为dom对象的方式有两种

  - jQ对象[0]------> 转化成了dom对象
  - jQ对象.get(索引)----->转化为dom对象

* j将DOM对象转化为jQ对象

  * $(dom对象)--------> 转化为jQ对象

* jQ

  * 获取页面的元素

    $('CSS选择器')

     css选择器

    标签选择器(div,img,a),,类选择器(class),相邻选择器,结构伪类选择器,id选择器 ,后代选择器

* jQ中使用自己的方法选中页面中的标签

  * eq(下标) ----> 选取第几个下标  有点类似于 nth-child() 
  * odd 选中奇数的元素 (索引号是奇数)
  * even 选中偶数的元素 (索引号是偶数)
  * jQ对象.parent()------->获取当前元素的直接父元素
  * jQ对象.parents()--->获取当前元素的所有的父辈元素
  * jQ对象.children([ '选择器'])--->获取当前元素中的所有的直接子元素
  * jQ对象.find(['选择器'']) --->获取当前元素中的子元素,子元素中包括直接子元素和间接子元素(类似于css中的后代选择器)
  * jQ对象.siblings(['选择器'])---->获取当前元素的所有兄弟元素
  * jQ对象.hasClass('类名')----->获取当前元素中有没有某个类名   返回Boolean值
  * jQ对象.eq(下标) ---->获取指定索引的标签  
  * $(this).index()  ----->通过jQ获取当前li的索引值   
  * ul.show()---->显示下拉框   

* 注意:

  * jQ元素.parents('选择器')------>获取所有父辈元素中的指定的父元素
  * 选择器必须使用   引号

## 6.jQ中操作页面中元素的样式

* 语法:    这就是隐式迭代

* jQ对象.css('属性','属性值')  |  jQ对象.css({属性:'属性值',属性:'属性值'}) 

* 可以动态的给标签添加类样式实现样式的操作

  * jQ对象.addclass('类名')---->添加样式  类似于classList add()

  * jQ对象.removeClass();----->移除所有的类名

  * jQ对象.removeClass('类名')---->移除指定的类名;

  * jQ对象.toggleClass('类名')---->如果当前元素有这个类名,就移除,没有就添加

  * 注意

    * 1.如果通过addClass() 给元素添加多个类名,那么类名中间使用空格隔开

      ```js
      $('div').addClass('box text')
      ```

    * jQ对象.addClass().addClass()

* 隐式迭代:jQ 自己内部就可以将数组进行遍历,不需要我们手动遍历

注意:组织页面跳转的第一种方式   javascript:;

```js
//第一种
<a href="javascript:;"></a>

//第二种
  a.onclick=function(){
     return false; 
    }
```

## 7.jQ动画效果

    1. 元素的隐藏和显示

    * hide(参数1 ,参数2, 参数3)  隐藏
      * 参数1 speen: 动画的速度类型('slow','normal','fast'  | 设置后一个毫秒值)
      * 参数2  easing:设置动画切换效果('linear','swing')
      * 参数3 fn : 代表动画完成后的一个回调函数
    * show() 显示

    2. 滑动效果

    * slideDown(): 向下拉
    
    * slideUp(): 向上走
    
    * 注意:
    
      * slideUp 也可以隐藏元素,通过改变元素的高度
      * slideDown() 显示元素,可以改变元素的高度	

    3. 淡入淡出效果

    * fadeIn() 淡入
    * fadeOut() 淡出
    * 注意:
      * fadeIn() 通过控制元素的透明度实现显示元素
      * fadeOut() 通过控制元素的透明度隐藏元素
    * fadeTo(参数1,参数2,参数3,参数4)
      * 参数1: 动画的速度类型('slow','normal','fast'  | 设置后一个毫秒值)
      * **参数2 opacity(透明):代表透明度, 必须设置,取值是0-1之间**

    4. 自定义动画

    * 语法: animate(参数1,参数2,参数3,参数4)
      * **params:代表属性和值  (css中的属性和值)  必填设置**
      * 注意:
        * 1.animate中不能直接设置与颜色相关的动画效果

# day2

## 动画排队的问题

在动画执行之前使用  stop()   停止动画

注意:

* 1.以后我们在使用jQ动画的时候,在动画前面一定加stop()

## jQ方式操作标签的属性

1.通过jQ的方式操作元素本身固有的属性

​	获取

​		jQ对象.prop('属性') 获取元素上的值

```js
//获取div的class属性值
$('div').prop('class')
```

​	设置

​		jQ对象.prop('属性名','值')

```	js
//设置div的class的值
$('div').prop('class',123)
```

2.通过jQ获取标签的自定义属性

​	获取

​		jQ对象.attr('自定义属性')

```js
//获取标签的自定义属性
$('div').attr('data-age')
```

​	设置

​		jQ对象.attr('属性名','值')

```js
$('div').attr('myname','text')
```

## 获取标签中的值

​	获取/设置 表单控件中的值

​		 jQ对象.val()------->获取

```js
$('input').val();
```

​		jQ对象.val('345')------>设置

```js
$('input').val('值');
```

​	获取/设置  非input标签的值

​		jQ对象.text()---------->获取标签中的内容,特点与原生js中的  innerText一样

​		jQ对象.html()---------->获取标签中的内容,特点与原生js中的  innerhtml一样

```js
$('div').text()
$('div').html()
```

​		jQ对象.text('值 ')-------->设置标签中的值

​		jQ对象.html(值)-------->获取标签中的值,可以设置标签

```js
$('div').text('我是span标签')
$('div').html('我是span标签')
```

tofixed(2) 保存2位小数

实现用户手动输入,修改对应的总价

change 修改   手动输入修改 事件

## jQ对象的遍历   (遍历jQ对象里面的值)

语法:

* jQ对象.each(function(i, item){ })

  形参i: 代表每一个对象对应的索引值

  形参item: 代表每一个DOM对象

  $(item) 转成jQ对象 

## jQ中如何操作元素

* 创建元素
  * jQ对象.html()
  * $('html标签')
  * 步骤:
    * 1.先创建元素: $('html标签')
    * 2.将创建的元素追加到父元素中
      * jQ对象.append(创建的元素)----->将创建的元素添加到父元素的结束位置
      * jQ对象.prepend(创建的元素)------>将创建的元素添加到父元素的开始位置
* 添加兄弟元素
  * jQ对象.after(创建的元素)----->将创建的元素作为当前元素的兄弟元素,在当前元素的后面
  * jQ对象.before(创建的元素)----->将创建的元素作为当前元素的兄弟元素,在当前元素的前面

* 删除元素
  * jQ对象.remove()------> 将当前的元素删除
  * jQ对象.empty()--------> 将当前元素中的内容清空
  * jQ对象.html(' ') --------> 将当前标签内的内容清空



# day3 今日重点:

# ***对数据进行增删改查

## jQ设置和获取缓存数据

```js
//在程序中,将数据保存下来方式:

//变量,数组,对象,本地存储,自定义属性

语法:
	jq对象.data('属性名')
	jq对象.data('属性名','值')
本质
	jQ对象.data()方法也是在操作自定义属性,将数据保存到了缓存中,没有在标签上体现出来
```

## jQ遍历

```js
$.each(object(遍历的对象),function(index,element){})
```

备注:

* 1.object表示要遍历哪个对象,一般在程序是一个数据[数组,对象]
* 2.index,表示数据的索引值
* 3.element 表示数据中的值

区别:

* 1.$.each() 去遍历数据  一般情况下用来遍历数组(也可以遍历jQ对象)
* 2.jQ对象.each() 去遍历数据,一般情况下 就是用来去遍历jQ对象的

```js
例如:
//遍历程序中的数据
 $(function() {
    var arr = ['a', 'b', 'c'];
    $.each(arr, function(i, element) {
      console.log(i, element);
    })
  })
//输出: 0 'a'   1 'b'  3 'c'
```



## jQ获取元素的大小和位置

```js
语法:
获取元素大小方法如下:

1.jQ对象.width() |  Q对象.height()   ---->获取 内容区域的大小

2.jQ对象.innerWidth()  |   jQ对象.innerHeight()----->获取内容区域+内边距的大小

3..jQ对象.outerWidth()  |   jQ对象.outerHeight() ---->获取元素大小(内容区域+内边距+边框)  实际大小

4..jQ对象.outerWidth(true)  |   jQ对象.outerHeight(true) ---->获取元素大小 (内容区域+内边距+边框+外边距)
```

注意:

   	1. 如果要通过 width() 设置值, 写法:  jQ对象.width(值)
   	2. 在设置值的时候,不需要加单位;

```js
  // 获取元素大小
  $('.box').width(); //输出200
  $('.box').height(); //输出200
  console.log($('.box').innerWidth()); //输出206
  console.log($('.box').outerWidth()); //输出216
  console.log($('.box').outerWidth(true)); //输出416
```

获取元素位置如下:

1.jQ对象.offset()   返回 一个对象

​	得到的是一个对象

​	left:        top:

​	总结:

​		通过offset()得到元素的位置,与其父元素无关,通过offset()获取的是当前元素相对整个文档(页面)

```js
$('.one').offset().left
$('.one').offset().top
```

2.jQ对象.position()   返回一个对象

​	得到的是一个对象

​	left:   |    top:

​	总结:

​		通过position() 获取元素位置的时候,如果当前父元素没有定位,那么就参照整个文档(页面),,如果当前父元素有定位,那么就参照父元素(类似于css中的绝对定位)

```js
$('.one).position().left;
$('.one).position().top;
```

3.jQ对象.scrollTop();    返回具体值

​	scrollTop() 用来获取内容区域(元素)滚动出去的距离

​	如果希望通过程序的方法获取元素滚动出去的距离,那么需要在scroll事件中获取

​	该方法返回就是一个滚动出去的距离的具体值

## jQ注册事件

1.常规方式通过:  事件源.事件类型(function(){});   一次只可以注册一个事件,没办法给动态创建元素注册事件

例如:$('div').onclick(function(){})

2.通过on的方式给元素注册事件

事件源.on('事件类型','选择器',function(){})

事件源.on({

​	事件类型:function(){},

​	事件类型:function(){},

​	事件类型:function(){}

})

```js
$('div').on('事件类型',function(){})
$('div').on('click',function(){
    $(this).css('background','pink');
})

$('div').on({
    click:function(){
        $(this).css('background','pink')
    },
    mouseenter:function(){
        $(this).css('background','red')
    }
})
```

## jQ解绑事件

语法: 

​	jQ对象.off()

总结:

 1. 如果off()方法中没有设置任何参数,那么代表将该对象中的所有事件都解绑

 2. 如果要通过off() 方法移除对应的事件,那么在参数中设置对应事件的名称即可

    1. 例如:  $('div).off('click');

    2. 如果要将委托事件解绑,那么介意按照如下写法

    解绑委托事件

​	$('父事件源').off('事件源','选择器')

​	$('.box').off('click','.one')

   	4. 可以给元素通过  one() 方法给元素注册事件,但是只能执行一次

## jQ自动触发事件

第一种自动调用的方式:



事件源.事件类型( )     $('div').click()

//自调用函数:让函数自己调用自己

自调用方式二:

事件源.trigger('事件类型')       $('div').trigger('click')

事件对象参数:当我们在执行某个事件的时候,会将用户的一些行为动作数据保存起来--->保存在   事件对象参数中

阻止事件冒泡

e.stopPropagation()

## 其他部分

1.拷贝对象

​	语法:

​		$.extend([deep],targetObject , currentObject)  

​		参数介绍:

​			1.deep,  布尔类型的值,  默认值是 false  该参数用来设定拷贝对象的时候是深拷贝,还是浅拷贝

​				如果deep的值是默认值,代表的是浅拷贝

​				如果deep的值 是true  代表的是深拷贝

​				总结:

​					1.不管是深拷贝还是浅拷贝,如果原来对象中有一个和被拷贝对象中相同的属性,会被覆盖掉

​					2.不管是深拷贝还是浅拷贝,如果原来对象中不存在与被拷贝对象相同的属性,不会被覆盖掉

​					3.如果是浅拷贝,那么在拷贝过程中如果遇到事对象,那么是将对象的地址赋值给目标对象

​					4.如果是深拷贝,那么在拷贝的过程中 是直接将对象复制一份拷贝给目标对象

​			2.targetObject 用来接收拷贝的对象

​			3.currentObject 要被拷贝的对象

2.多库共存:  为了避免其他js文件中的命名和jQuery中的$命名冲突

​			1. 将 $ 用 jQuery 替换

​			2. 通过自定义的方式实现

​				var 自定义一个变量=jQuery.noConflict()

​				自定义一个变量('div')...

​		3.插件介绍:

​			全屏滚动插件

​			懒加载插件

​			插件使用步骤一般注意事项:

​				1.必须先引用jQ文件

​				2.然后在引用当前的插件对应的js文件

简单数据类型:  属性 值

复杂数据类型: 对象 {}     复制的话 只是复制的地址

​			2.targetObject 用来接收拷贝的对象

​			3.crrentObject  要被拷贝的对象

​	

*** 要根据索引值获取对应的内容区域盒子

$('li').eq(index);

localStorage.getItem('malist');  获取本地存储中的数据

## window的一个方法  window的去向

window.location.href='./index.html'











