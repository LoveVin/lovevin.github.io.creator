---
title: "JS对象分类"
date: 2020-01-31T19:53:30+08:00
tags: ["JS对象"]
categories: ["JavaScript"]
draft: false
---

## 1. 为什么要分类？

JS将数据分为七种数据类型，四基两空一对象，即四个基本数据类型number、string、bool、symbol，两个空数据类型undefined、null，一个对象数据类型。对象数据类型很复杂，但对象数据类型与现实生活的数据信息表示地最为准确，因此用到更广泛。根据实际生活中的数据有分类，JS也将对象数据类型再次细分为不同类型的对象，每类对象抽象出共同属性存放至其原型中。

JS将对象进行分类方便于管理对象，并且JS的创建之初就已经划分出了几类对象，如普通对象Object、数组队形Array、函数对象Function、日期对象Date等等。并且，JS允许用户自定义一类对象，具体实现方法可以用构造函数实现。

## 2. 构造函数

首先介绍一个问题引出构造函数，例如要创建5个不同宽度的正方形对象，并且每个正方形对象都有求周长和求面积的两个方法，可以想到用for循环的方式进行如下创建：

```javascript
let squareList = []
let widthList = [1,2,3,4,5]
for(let i = 0; i<5; i++){
    squareList[i] = {
        width: widthList[i],
        getArea(){
        	return this.width * this.width
        },
        getLength(){
        	return this.width * 4
        }
    }
}
```

以上方法会浪费内存，重复创建getArea()函数和getLength()各5次，但其实这些正方形的求面积和求周长的方法是一样的，因此可以抽象出来放到正方形的原型函数中，修改后如下所示：

```javascript
let squareList = []
let widthList = [1,2,3,4,5]
let squarePrototype(){
    getArea(){
        return this.width * this.width
    },
    getLength(){
        return this.width * 4
    }
}
for(let i = 0; i < 5; i++){
    squareList[i] = Object.create(squarePrototype);
    squareList[i].width = widthList[i];
}
```

以上借助原型的概念将正方形的共同属性抽象出来放到原型中，大大节省了内存空间，但以上代码还可以通过传参的形式再优化修改如下：

```javascript
let squareList = []
let widthList = [1,2,3,4,5]
let squarePrototype(){
    getArea(){
        return this.width * this.width
    },
    getLength(){
        return this.width * 4
    }
}
function createSquare(width){
    let obj = Object.create(squarePrototype);
    obj.width = width;
    return obj;
}
for(let i = 0; i < 5; i++){
    squareList[i] = createSquare(widthList[i]);
}
```

以上代码看起来优化很多，但存在的问题是构造函数和原型函数之前看起来没有什么关系，因此可以将构造函数和其原型函数之间联系起来，采取的方法是将原型函数作为构造函数对象的一个方法，并在原型函数中记录其对应的构造函数是谁，继续修改如下：

```javascript
let squareList = []
let widthList = [1,2,3,4,5]
createSquare.squarePrototype(){
    getArea(){
        return this.width * this.width
    },
    getLength(){
        return this.width * 4
    }
    constructor: createSquare
}
function createSquare(width){
    let obj = Object.create(createSquare.squarePrototype); //new字符会帮忙写
    obj.width = width;
    return obj;
}
for(let i = 0; i < 5; i++){
    squareList[i] = createSquare(widthList[i]);
}
```

因此根据以上优化后的代码，JS将其封装起来统一定义，用new操作符调用构造函数创建对象，并且将每个构造函数中的指向原型函数的属性统一定义为prototype属性，将每个prototype中指向其构造函数的属性统一定义为constructor，将构造函数和原型函数相互联系了起来，并且prototyp的constructor指向构造函数自己。因此JS在设计的过程中，给每个函数对象都添加了一个prototype属性，指向其作为构造函数时的原型对象用于存放公共属性，和\_\_proto\_\_属性没有什么关系，**例如Object 的原型是指 Object.__proto__，不是 Object.prototype，因为 Object.prototye 是 Object 构造出来的对象的原型**，_\_proto\_\_是JS规定每个对象都必须有原型并用该属性存储，函数对象也属于对象，才会有此属性。因此  构造函数的prototype === 实例对象的\_\_proto\_\_，因此写一个构造函数定义一类对象的方式如下所示，这样定义的构造函数命名首字母一般大写。

```javascript
let squareList = []
let widthList = [1,2,3,4,5]
function Square(width){
    this.width = width
    this.sum = function(){
        //do something
    }
} //构造函数，其中属性为=赋值语句，添加新对象自身属性或方法
Square.prototype.getArea = function(){
    return this.width * this.width
}
Square.prototype.getLength = function(){
    return this.width * 4
}  //添加新对象共用属性
for(let i = 0; i < 5; i++){
    squareList[i] = new Square(widthList[i]);
}
```

以上就是正确定义构造函数自定义一类对象的方法，通过new操作符省略用原型创造对象并返回对象的操作，直接让用户在构造函数中定义自己的属性，在其prototype属性中定义公共属性，并用new操作符创建对象即可。那么操作符在创建对象时做了什么？如下：

let obj = new X()

1) 自动创建空对象

2) 将空对象与原型关联，空对象原型地址_\_proto\_\_值指定为X.prototype值

3) 自动将新创建的空对象作为this关键字运行构造函数

4) 自动return this

得到以下公式：

##### 对象\. _\_proto\_\_=== 其构造函数.prototype

## 3. 代码规范

由以上构造函数的形成过程可得出一般约定俗成的命名规法如下：

1) 构造函数的命名为名词，且首字母大写

2) 普通函数的命名以动词开头，且首字母小写

3) 所有被构造出来的实例对象，首字母小写。

## 4. class新语法

class语法是ES6新增加的语法，将上述构造函数代码修改如下：

```javascript
class Square{
    
    constructor(width){
        this.width = width
    } //构造函数
    
    kind = 'shape' //公有属性为赋值语句，且每个属性之间没有逗号
    'kind2' = 'Rectangle'
    
    getLength:function(){
        return this.width * 4
    } //公有方法，且每个方法之间没有逗号

    getArea(){
        return this.width * this.width
    } //公有方法，简写定义方法，常用。

    get area2(){
        return this.width * this.width
    }  //get 函数名，该函数设置为只读属性，调用函数area2时不用加()，只需.area2即可调用
}
```

