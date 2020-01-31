---
title: "JS对象之普通对象"
date: 2020-01-31T19:54:57+08:00
tags: ["JS对象"]
categories: ["JavaScript"]
draft: false
---

## 1. 对象的定义

#### 属性名和属性值

对象是用来描述一个物体及其相关属性的集合体，里面是以键值对表示的无序的数据集合，键值对是指用键值名:键值的方式存储数据，在JS中又称之为属性名：属性值。且JS中的属性名是普通字符串而不是标识符，可以是任意字符，但如果属性名省略引号，则必须是标识符了。而属性值根据传入的数据类型定义类型，如数字、字符串、对象等等类型。(标识符与字符串的区别看XXX)

对象的定义方式如下：

```javascript
let obj = new Object({'name': 'haha', 'gender': 'man'}) //对象的正确创建方法

let obj = {'name': 'haha'} //对象的简写创建方法
```

**Object.keys(obj)可以得到obj这个对象的全部键值名**

**键值对在对象中成为属性名: 属性值，属性名一定为字符串，若想以变量的值作为属性名可以用[变量]取到该变量对应的值，也就是说，不加[]是将属性名自动变成字符串，加了[]就取变量中的值转为字符串**

**各属性间用逗号','分隔开**

#### 属性值可以为函数

在JS中，属性的值可以为函数，此时称该属性为方法。具体书写方式如下:

```javascript
//在对象创建时添加方法
let myObj = {
  myMethod: function(params) {
    // ...do something
  } //这是实际完整写法
  
  // 或者 这样写也可以
  
  myOtherMethod(params) {
    // ...do something
  } //该方法是ES5之后的更为简洁的定义方法的语法
};


//在对象创建完后添加方法
let myObj = new Object();
myObj.myNewMethod = function(params){
    // ...do something
} 
```

## 2. 对象的组成

每个对象在被创建后，其中包含的内容除了用户自定义的属性外，还都有一个共同的属性名"\__proto__"，该属性值是一个对象的地址，这个对象是该类对象的共同属性组成的对象，在JS中称之为该类对象的原型。隐藏属性存储着原型对象的地址。只要包含该隐藏属性，就可以直接使用原型对象中的属性和函数。

## 3. 对象属性的操作

#### 3.1 删除操作

##### 删除xxx属性值

obj.xxx = undefined

该操作实际上是将obj对象的xxx属性值删除，其实是赋值为空

##### 删除xxx属性

1) delete obj.xxx

2) delete obj['xxx']

以上两种操作会将obj这个对象的xxx属性删除，属性删除，该属性值也不存在，且在JS中delete操作就是用来删除对象的属性的

##### 检测删除是否成功

1) 'xxx' in obj == false //查看xxx是不是obj的属性名，返回值为false表示该属性删除成功

2) 'xxx' in obj && obj.xxx === undefined  //查看xxx是不是obj的属性，并且属性值是否是undefined

3) 只用obj.xxx === undefined，无法判断obj对象中是否含有xxx属性，因为当没有该属性时，其值自然是undefined，若有该属性，属性值为undefined，因此两种情况无法区分。

#### 3.2 读操作

1) Object.keys(obj)：查看obj对象的所有属性名

2) Object.values(obj)：查看obj对象的所有属性值

2) obj | Object.entries(obj)：查看obj对象的所有属性和属性值

以上三种方法仅仅可以看到对象自己定义的属性，看不到所在原型中的公共属性，若想查看公共属性，如下：

1) console.dir(obj) //以目录形式输出obj

2) obj.\__proto__

查看某属性是自己的属性还是公有的属性的方法：

obj.hasOwnProperty('xxx')   //是自己的属性返回true，共有属性返回false

##### JS中的任何对象都有原型，原型也是个对象，原型对象也有原型，只不过被人为定义为null空

##### 查看单个属性

1)中括号法： obj['属性名']      (中括号内为字符串)

2) 点法：obj.属性名 (属性名是字符串)

3) 变量中括号法  obj[name]    (中括号内为变量名，且则此变量要已经赋值，最终会变成字符串)

##### 注意：obj['name']和obj.name的区别，obj[name]中的name是变量，可改变，而obj.name是指的就是字符串为name的属性。因此，若想动态获取属性则可选择中括号的方式。

#### 3.3 写操作

写操作的语法和读操作的语法是一样的，读出来直接赋值即可，如obj.name = 'hehe'，obj['name'] = 'hehe'，且对象属性写入时无法修改原型的属性，只能修改自己的属性。

**批量赋值**：

JS的批量赋值是ES6新出的一个功能API，具体用法为Object.assign(对象名, {属性: 属性值})，例如：

Object.assign(obj, {name: 'hehe', age: 18})

若想要修改对象的原型，则可通过以下方式：

1) obj.\__proto__.toString(原型属性名) = 'xxx'   //这样会轻易改变所有原型的属性，使得原型会乱

2) Object.prototype.toString(原型属性名) = 'xxx'

## 4. 原型链

由上述操作可知，每一个对象都有一个隐藏属性\_\_proto\_\_，该属性存储的是一个对象的地址，该对象里是该类型对象的公共属性，因此称\_\_proto\_\_指向的对象为原型。原型对象可通过修改\_\_proto\_\_属性值来修改，指向另外一个自定义的公共属性对象，如下所示：

```javascript
var common = {nation: 'China', eyecolor: 'black'}
var person = {name: 'hehe', gender: 'man'}
person.__proto__ = common

得到的person的组成为：

person{
   name: "hehe"
   gender: "man"
    __proto__:
		nation: "China"
		eyecolor: "black
        __proto__: Object
}
```

这样就自定义了直接原型对象，但每一个对象都有原型，自定义的原型对象也有一个原型是Object，因此这样就成了在对象和原型之间添加了自定义的原型对象，形成了原型链。但是，直接修改\_\_proto\_\_属性是不安全的，因此在新版的ES6中新增了一种创建自定义原型的方法，如下所示：

```javascript
var common = {nation: 'China', eyecolor: 'black'}
var person = Object.create(common, {name: {value: 'hehe'},gender: {value: 'man'}})
// var person = Object.create(common)
// person.name = 'hehe'
// person.gender = 'man'

//也会得到和上述一样的person组成，这样在创建对象时就指定原型，而不是先创建对象，再修改原型，这样更安全，是最新版本的创建原型的方法，推荐使用
```

## 5 . 原型与对象

1) 以下方法创建对象是修改了直接原型并创建的其原型的属性

var person = Object.create({nation: 'China'}) 

2) 以下方法创建对象是创建的自己本身的属性

var person = new Object({name: 'hehe'})





