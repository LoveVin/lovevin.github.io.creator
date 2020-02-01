---
title: "JS三座大山之this"
date: 2020-02-01T21:48:33+08:00
tags: ["this"]
categories: ["JS三座大山"]
draft: false
---

## 1. this是什么

在JS中，每个函数都有一个隐藏的属性叫做this，其属性值默认是对象的地址，用于指向一个对象。通常情况下this常用于用作构造函数的函数中，普通函数一般用不到this属性。普通函数中用不到的this通常指向的是window对象，因为调用它的是window对象。构造函数中的this是用于指定未知的对象，当一个对象obj通过构造函数构造出来时，该对象中的this属性就是指向该对象本身。

##### 注意箭头函数没有this，其余函数都有this

## 2. 自定义this

#### 2.1 强制封装成对象

this指向的对象一般是随函数或者对象的创建而内定的，只有通过一个接口可以修改this指向的对象，即

```javascript
functionName.call(自定义this值，arguments值) 
functionName.call(自定义this值)

//或者
functionName.apply(自定义this值，[arguments值]) 
//该方法的arguments值必须用中括号[]包含起来
```

而且，this接收的值只能是对象，因此若通过call指定的this值不是对象类型，如是number类型1，那么JS会自动将1封装成对象。

#### 2.2 不要给我强制封装

当然了，也可以通过修改，告诉JS不让其将自定义的this值强制封装成对象，那么就是如下方法：

```javascript
function fn(){
    'use strict' //就是添加这句话
    console.log(this);
}
```

那么this值就是1，不会被封装成对象，不过这样做没什么用，只是有这样的实现方法而已。

#### 2.3 bind函数绑定this

函数有一个bindAPI，可用于this指向的对象和arguments值，这样可以让this始终指向一个固定的对象

```javascript
function f1(){
	console.log(this);
}
f1.bind({name:'haha'});
let f2 = f1;
f2(); //f2() === f1.call({name:'haha'})
```

## 3. 为什么要用this

由以上可知，this是用来指向一个未知对象的，那么为什么会用到一个未知对象呢？情况其实是，假如我们自定义一个功能为自我介绍的函数，即函数里输出一个对象的name属性，那么这个对象可能还没有被创建出来，不知道这个对象怎么能输出其名字呢？因此就用到了给该函数设置一个形式参数当作该对象放那里，直接写输出形式参数的name属性，当该对象被创建出来时，该对象在调用自我介绍函数的同时将自己作为参数传入函数，这样就能正确自我介绍了。

因此this就是上述函数中对象形参的演变，JS给每个函数统一规定了这样一个隐形参数this，每个对象在调用一个函数时都会将对象本身作为参数传入，在函数中就以this这个隐形形参接受该对象，并对其进行各种操作。也就是说，我们在调用一个函数时，尽管写的是 obj . functionName(); 看似没有传参，但实际上JS已经将调用该函数的对象obj传入函数了，并被函数的this属性接收。

那么为什么说this指向的对象未知呢？因为你不知道谁会调用这个函数，A调用这个函数那this就是指向的A，并且通过this对A进行操作。B调用这个函数那this就是指向B了，并对B进行操作。

## 4. 函数的两种调用方法

既然知道了this是什么和用来干什么的，那么对于函数的调用其实有两种形式：

#### 4.1 看不到this的常用法

函数的常用调用方法就是看不到隐藏属相this的产生过程，常用调用方法如下：

```javascript
A.sayHi(); //默认是将A作为this调用sayHi函数
```

#### 4.2 看到到this的清晰法

知道this的实际产生原理后可以用自己看得到this值的方法调用函数，如下：

```javascript
A.sayHi(A); //这种方法在JS中是错误的，JS不允许这样指定this

A.sayHi.call(A, arguments); //这样才是正确指定this的方法，即将A作为this调用sayHi函数

//注意使用call的时候要传参数时一定要写上传的this值，否则就将第一个arguments参数当作this了
```

所以我们看到，放在对象里的函数的this和该对象没什么关系，this只和调用该函数的对象有关，当然了，放在该对象里的函数只是该对象的属性，只能被该对象调用，可用call指定，不过没必要。

普通函数调用时没有指明对象名字，如add(1,2)。那是默认window对象调用的，所有函数的调用都需要对象调用的，并且该函数必须是作为其调用对象的属性获取到的。

##### 函数只有作为对象的属性才能被调用到

## 5. 对象创建符new

在JS中规定，用new操作符创建出来的对象的this就是指向该新创建的对象，这是new操作符决定的。因此如下所示：

```javascript
let obj = new Object();

//则this指向的对象就是新创建得到的obj对象
```

## 6. 理解this后

在理解了this后，JS中的某些API的具体实现就可以明了了，如数组的forEach遍历接口的实现：

```javascript
//forEach的this实现
function forEach(fn){
    for(let i = 0; i < this.lenght; i++){
        fn(this[i],i,this)
    }
}

//forEach的隐式常用法
array.forEach((item) => console.log(item))
array.forEach(function(item){
    console.log(item);
})

//forEach的清晰使用法
array.forEach.call(array, (item) => console.log(item))
array.forEach.call(array, function(item){
    console.log(item);
})
```





