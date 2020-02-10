---
title: "DOM的API"
date: 2020-02-10T14:05:32+08:00
tags: ["DOM API"]
categories: ["DOM"]
draft: false
---

## 写在前面

DOM的全称是Document Object Model(文档对象模型)，是浏览器提供给JS用来操作整个html页面的元素的，在JS中通过`window.document`语句获取。基本原理就是浏览器将整个网页抽象成一个DOM，并通过树的数据结构划分页面元素。

## 1. 获取页面元素的API

#### 1.1 获取元素标签

需要兼容IE浏览器的必须用document.getElementByxxxxx语法。

##### 1)）通过id获取

```javascript
window.idxx;

idxx; //widow可省略，当id名为全局属性名关键字时不可用这种方法

document.getElementById('idxxx');
```

##### 2）通过class获取

```javascript
document.getElementsByClassName('classxxx'); //获得到的是一个class值为classxx的元素数组

document.getElementsByClassName('classxxx')[i] //获得第i个元素
```

##### 3）通过标签名获取

```javascript
document.getElementsByTagName('xxx'); //获得的是一个xxx标签元素数组，如div/span

document.getElementsByTagName('xxx')[i]; //获得第i个元素
```

##### 4）通过JQuery选择器获取

```javascript
document.querySelector('#idxxx'); //通过id获得单个元素

document.querySelectorAll('.classxxx')[i]; //通过class名获取元素数组

document.querySelector('div > span:nth-child(2)'); //里面通过css的获取方法获取元素

document.querySelectorAll('div > span:nth-child(2)'); //获取数组
```

#### 1.2 获取页面元素

##### 1）获取html标签

```javascript
document.documentElement
```

##### 2）获取head元素

```javascript
document.head
```

##### 3）获取body元素

```javascript
document.body
```

##### 5）获取窗口(窗口不是元素)

```javascript
window
```

##### 6）获取所有元素（可用于判断浏览器类型）

```javascript
document.all //该值是一个falsy值

//可用于判断当前浏览器是否是ie浏览器，该值在ie浏览器的ie11之前的版本中都是真，在其他浏览器是假，在其他浏览器可以直接用，该语句可以判断是否是ie11之前的版本，新的ie11也是假了。

if(document.all){
    console.log('ie11之前的ie版本');
}
else{
    console.log('ie11或Edge其他浏览器');
}
```

## 2. DOM获取的元素的原型链

显然，根据浏览器提供的DOM接口可以获取到html页面的元素，获取到的元素很显然是一个对象，拥有很多自身属性和公有属性，搞清楚共有属性，那就需要搞清楚该元素的原型链，以一个DOM获取到的div元素的原型链展示，具体如下：

##### 1）第一层原型是HTMLDivElement.prototype

里面是所有div元素共有的属性

##### 2）第二层原型是HTMLElement.prototype

里面是所有HTML标签(也叫元素)共有的属性

##### 3）第三层原型是Element.prototype

里面是浏览器支持的所有文件如HTML、XML、SVG标签的共有属性

##### 4）第四层原型是Node.prototype

里面是所有节点共有的属性，节点包括浏览器支持的所有文件类型的标签、文字、注释等等。因此可知文字是节点，不是标签，注释也是节点。

##### 5）第五层原型是EventTarget.prototype

里面是所有节点事件相关的属性，比较常用的属性是addEventListener。

##### 6）第六层也是最后一 层原型是Object.prototype

终极原型，所有原型的祖先，到这几没了。

## 3. 节点的增删改查

#### 3.1 增

##### 1）创建一个标签节点

`document.createElement('xxx');`

例如 `div = document.createElement('div');`

##### 2）创建一个文本节点

`document.createTextNode('stringxxx');`

例如 `text = document.createTextNode('这是个文本');`

##### 3）标签里插入文本

##### 在JS中创建的节点默认是处在JS线程中，必须添加到html中的元素中才能生效，并且一个节点只能添加到一个元素中，不能一个节点添加到两个元素中，除非复制一份。

`标签节点.appendChild('文本节点');`

例如 `div.appendChild(text);`

```javascript
div.innerText = "这是个文本"

div.textContent = "这是个文本" //这两种方法都可以改文本内容

但是不能是div.appendChild('这是个文本')
```

##### 4）克隆节点

`新节点 = 节点.cloneNode();`

例如`div2 = div.cloneNode();`

#### 3.2 删

##### 1）旧方法，只能由父亲删除自己

这种方法需要先找到要删除元素的父元素，让其父元素删除它，这种删除只是将其从html中删除，节点还在内存中，可随时再添加，彻底删除的方法是将该删除节点置为空即可被内存管理回收。

`要删除节点.parentNode.removeChild(要删除节点);`

`父元素节点.appendChild(删除的节点);`

##### 2）新方法，可自己删除自己，IE不支持

`要删除节点.remove();`

#### 3.3 改

##### 1）改id

`节点.id = '新id名';`

##### 2）改class

由于class是JS的关键字，所以不能直接节点.class修改，要如下方式：

**旧方法**

```javascript
节点.className = '新cass名字';`  //这样会完全覆盖原来的class属性值

节点.className += ' 新的class名'; //这样才会是添加class值，前面要有个空格
```

**新方法**

```javascript
//新方法的添加Class

节点.classList //可查看当前节点的所有class值

节点.classList.add('新的class名')
```

##### 3）改style

```javascript
节点.style = 'width: 100px; color: red;' //一下改多个样式

节点.style.width = '100px'; //修改单个样式

//JS不支持有中划线的key值，会被当成减号的，如background-color，则要以字符串形式表示或者改中划线为首字母大写

节点.style['background-color'] = 'red';

//or
节点.style.backgroundColor = 'red'; //或者首字母大写

//特殊地，该data-*开头的属性名的属性值时为
节点.dataSet.* = 'xxx';
```

##### 4）改属性

```javascript
//可直接通过节点.属性名来修改，
div.classList/a.href等

//但是有的属性这样获取会出错，如a.href，浏览器会补全路径，因此用如下方法：
节点.setAttribute('属性名','属性值');//该种方式最完整

节点.getAttribute('属性名'); //获得属性
```

##### 5）改文本内容

和增加文本内容是一样的语句

```javascript
div.innerText = "这是个文本"

div.textContent = "这是个文本" //这两种方法都可以改文本内容
```

##### 6）改HTML内容

```javascript
节点.innerHTML = 'html语句'
```

##### 7）改标签

改标签可以先用innerHTML将内容清空，再添加节点

```javascript
节点.innerHTML = '';

节点.appendChild(节点);
```

##### 8）改爸爸

```javascript
新爸爸节点.appendChild(节点); 

//这样就可以改变父亲节点，因为一个节点只能添加到一个节点上，因此该节点会被从原父亲节点移除，加入新的父亲节点下
```

#### 3.4 查（返回的是值）

##### 1）查爸爸

```javascript
节点.parentNode;
//or
节点.parentElement;
```

##### 2）查子代

```javascript

//查看所有孩子

节点.childNodes; //返回的是一个子节点数组，节点类型包括标签、文字、注释、多个回车或空格被html转化成的一个空格也是其子节点

//or

节点.children; //解决了childNodes的问题，是Element提供的，只计算元素，即标签节点

//查看单个孩子

节点.firstChild; //查看第一个孩子

节点.lastChild; //查看最后一个孩子

```

##### 3）查兄弟姐妹

DOM没有提供查找所有兄弟姐妹节点的API，可以通过查看其父亲节点的所有孩子节点，再排除掉自己，只提供了查看临近兄弟姐妹的API

```javascript

节点.parentNode.childNodes; //不仅排除自己还要排除文本节点

节点.parentNode.children; //排除自己

节点.previousSibling; //临近的上个兄弟节点可能有文本节点

节点.nextSibling; //下个兄弟节点，可能有文本节点

节点.previousElementSibling; //上一个元素兄弟

节点.nextElementSibling; //下一个元素兄弟

```

















