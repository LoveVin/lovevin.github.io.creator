---
title: "jQuery的API"
date: 2020-02-10T14:01:57+08:00
tags: ["jQuery API"]
categories: ["jQuery"]
draft: false
---

#### 1. 选择页面元素

jQuery的设计思想就是 [ 选择某个元素，然后对其进行操作 ]，因此，通过jQuery直接选择到元素得到的返回值是一个包含各种操作方法的对象，具体想对选择到的元素进行何种操作，只需调用对应的函数(接口)即可。

jQuery即$，只接受一个参数，这个参数有两种类型。

##### 1.1 CSS选择器

```

$(document) //选择整个文档对象

$('#myId') //选择ID为myId的元素

$('.myClass') // 选择class为myClass的元素

$('input[name=first]') // 选择name属性等于first的input元素

```

##### 1.2 jQuery特有表达式

```

$('a:first') //选择网页中第一个a元素

$('tr:odd') //选择表格的奇数行

$('#myForm :input') // 选择表单中的input元素

$('div:visible') //选择可见的div元素

$('div:gt(2)') // 选择所有的div元素，除了前三个

$('div:animated') // 选择当前处于动画状态的div元素

```

#### 2. 过滤性选择元素

```

$('div').has('p'); // 选择包含p元素的div元素

$('div').filter('.myClass'); //选择class等于myClass的div元素

$('div').not('.myClass'); //选择class不等于myClass的div元素

$('div').first(); //选择第1个div元素

$('div').eq(5); //选择下标为5即第6个div元素

```

#### 3. 选择元素的亲戚们

```

$('div').parent(); //选择div元素的父元素

$('div').children(); //选择div的所有子元素

$('div').siblings(); //选择div的同级元素

$('div').next('p'); //选择div元素后面的第一个p元素

$('div').closest('form'); //选择离div最近的那个form父元素

```

#### 4. 元素的基本操作

**创建元素**

```

let newLi = $('<li class="new">new list item</li>'); //创建新元素

$('ul').append(newLI);//先创建再添加

$('ul').append('<li>list item</li>'); //直接添加

```

**清空元素内容**

```
$( ".hello" ).empty(); //清空class为hello的元素的所有子节点，但不删除元素
```

**删除元素**

```

$( ".hello" ).remove(); //删除class为hello的元素本身和其所有子节点。除了元素本身之外，还删除与元素关联的所有绑定事件和 jQuery 数据。

$(".hello").detach(); //与remove类似，不同之处是不删除与元素关联的所有绑定事件和 jQuery 数据。

```

**复制元素**

```
$( ".hello" ).clone();
```

#### 5. 元素的位置移动

元素的位置移动有两种方法，一种方法是直接移动该元素，另一种方法是移动其他元素，使得目标元素达到我们想要的位置。

假定我们选中了一个div元素，需要把它移动到p元素后面。

第一种方法是使用.insertAfter()把div元素移动p元素后面：

```
$('div').insertAfter($('p'));
```

第二种方法是使用.after()，把p元素加到div元素前面：

```
$('p').after($('div'));
```

表面上看，这两种方法的效果是一样的，唯一的不同似乎只是操作视角的不同。但是实际上，它们有一个重大差别，那就是返回的元素不一样。第一种方法返回div元素，第二种方法返回p元素。你可以根据需要，选择到底使用哪一种方法。

使用这种模式的操作方法，一共有四对：

```
.insertAfter()和.after()：在现存元素的外部，从后面插入元素

.insertBefore()和.before()：在现存元素的外部，从前面插入元素

子.appendTo()和父.append()：在现存元素的内部，从后面插入元素

子.prependTo()和父.prepend()：在现存元素的内部，从前面插入元素
```

#### 6. 取值赋值合一API

```
$('h1').html(); //html()没有参数，表示取出h1的值

$('h1').html('Hello'); //html()有参数Hello，表示对h1进行赋值
```

常用的取值赋值函数如下：

```
.html() 取出或设置html内容

.val() 取出某个表单input元素的值

.text() 取出或设置text内容

.attr(attributeName) 取出或设置某个属性的值

.width() 取出或设置某个元素的宽度

.height() 取出或设置某个元素的高度
```

需要注意的是，如果结果集包含多个元素，那么赋值的时候，将对其中所有的元素赋值；取值的时候，则是只取出第一个元素的值 (.text()例外，它取出所有元素的text内容）。

**.attr()**

```

$('h1').attr('class'); //获取h1元素的class值

$('h1').attr('class','newClass'); //设置h1元素的class值为newClass

$('h1').attr({
	'class': 'newClass',
	id: 'newId'
}); //设置h1元素的class和id等多个属性,class属性名必须加引号，其他随便

$('h1').attr('class',function(index, oldval){
	return 'new' + val + index;
}); //函数的index值是每个h1元素的下标，oldval是其旧的属性值，return返回新值，若不return或return undefined，则保持原有值不变

```

以上的取值赋值合一方法的赋值参数都可以是函数，函数中的参数值为index下标和oldval旧的值。

#### 7. 链式操作

```
$('div').find('h3').eq(2).html('Hello');

```

上述的链式操作一步步解释为：

```
$('div') //找到div元素

　　　.find('h3') //选择其中的h3元素

　　　.eq(2) //选择第3个h3元素

　　　.html('Hello'); //将它的内容改为Hello
```

后退一步到上个节点，用end()方法

```
$('div')

　　　.find('h3')

　　　.eq(2)

　　　.html('Hello')

　　　.end() //退回到选中所有的h3元素的那一步

　　　.eq(0) //选中第一个h3元素

　　　.html('World'); //将它的内容改为World
```

#### 8. 参考/推荐文章

阮一峰的《[jQuery设计思想](http://www.ruanyifeng.com/blog/2011/07/jquery_fundamentals.html)》

jQuery [中文文档](https://www.jquery123.com/)