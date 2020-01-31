---
title: "JS对象分类之数组"
date: 2020-01-31T19:56:02+08:00
tags: ["Array"]
categories: ["JavaScript"]
draft: false
---

## 1. 写在前面

在JS语言中，其实没有真正的数组这个数据类型，JS是用对象模拟数组的形式，在JS中，数组是一种对象下的一个分类，但在其他语言中，数组可能是一个数据类型，要区分开。典型的数组是严格要求数据的数据类型是统一 的，并且可以用下标获取。但JS中的数组中存放的数据的数据类型可以不统一，比如第一个放数字，第二个放字符串，第三个放对象等等都是可以的，JS是通过键值对的方式来模拟数组的。

## 2. 数组的定义

#### 2.1 数组的常规定义方法：

```javascript
var arr = new Array(3); //只有一个参数时为数组长度，此句为创建一个长度为3的数组
var arr = new Array(1,2,3); //超过一个参数时为属性值，此为创建一个长度为3且其中值为1,2,3的数组
var arr = [1,2,3]; //上一种形式的简写
```

#### 2.2 数组的非常规定义方法：

**1) 分割符：array = string.split**

将字符串进行分割，分割的字符组成一个字符串

```javascript
let str = 'a,b,c'
let arr = str.split(',')  //根据逗号将字符串分割形成数组arr

let str2 = 'abc'
let arr2 = str2.split('') //分割符为空，根据字符分割成数组arr2
```

**2) Array的API：array = Array.from(string)**

Array.from是最新的JS语法提供的API，作用是将不是数组的东西变成数组形式

```javascript
let arr3 = Array.from('123') //可以将字符串变成数组
let arr4 = Array.from(123) //不可以将数字变成数组
let arr5 = Array.from(true) //不可以将bool变成数组
let arr6 = Array.from({0:1,1:2,2:3,length:3}) //这样形式的对象可以变成数组，必须加length属性
```

**3) 数组合并：array = array1.concat(array2)**

通过两个array的合并得到新的数组，并且不会改变原有数组

```javascript
let arr1 = [1,2,3]
let arr2 = [4,5,6]
let arr3 = arr1.concat(arr2)
```

**4)数组切割： array = array1.slice(切割位置)**

```javascript
let arr = [1,2,3,4,5,6]
let arr1 = arr.slice(2) //从第二个位置开始切割，得到arr1 = [3,4,5,6]，并且不会改变原数组

let arr2 = arr.slice(0) //从第0个位置切割，即不切割，原样复制，常用于复制一个数组
```

#### 2.3 伪数组

伪数组指的是该对象类似于数组对象，但是其原型链中没有数组的原型，该对象也就没有数组对应的属性和API。如下所示创建的数组就是伪数组

```javascript
let arr8 = {0:1,1:2,2:3,length:3}
```

以上的2.1和2.2的常规和非常规定义的数组都是真数组，伪数组可以通过Array.from变成真数组

## 3. 数组的自身属性

1)  '0'、'1'、'2'、'3'、、、、：index属性，只要是属性名，都是字符串，因此index也是字符串

2)  length：长度属性

## 4. 数组的公有属性

数组的公有属性有很多，列举以下常用的属性

1) push(value)：往数组添加一个值，在栈顶进行。

2) pop()：与push相反，从数组弹出一个值，在栈顶进行。

3) shift()：提高数组栈底部基线，即删除栈底元素。

4) unshift(value)：与shift相反，从栈底插入一个元素。

5) join('x')：在数组字符间用x连接起来并返回连接后形成的字符串，不会影响原有数组。

6) arr1.concat(arr2)：将arr1数组和arr2数组连接起来**返回一个新的数组**，不会影响原有数组。且concat不仅可以接受一个数组，也可接受一个数，就是将该数push进数组的意思

## 5. 数组的操作

#### 5.1 删除操作

1) 删除属性(错误)

数组也是对象，数组属性的删除可用对象属性删除的方法。如下所示：

```javascript
let arr = [1,2,3,4]
delete arr[0] // delete arr['0'] 是一样的，不加引号，也会自定将下标转为字符串
//这样删除，原有数组的length长度不会改变，还会留出一个empty空位置，这样就成了稀疏数组
```

2) 改length(错误)

```javascript
let arr = [1,2,3,4]
arr.lenght = 2 //这样就把后面的3和4删除了，length也修改为了2
```

3) 用shift删除第一个元素

```javascript
let arr = [1,2,3,4]
arr.shift() //arr = [2,3,4]，从栈底删除一个元素，且长度会变
```

4) 用pop删除最后一个元素

```javascript
let arr = [1,2,3,4]
arr.pop() //arr = [1,2,3]，从栈顶删除一个元素，且长度会变
```

5) 用splice删除中间元素(**splice强大且重要**)

```javascript
let arr = [1,2,3,4,5,6]
arr.splice(2,1) //意思是从下标为2的位置开始删除1个元素得到 arr = [1,2,4,5,6]
//arr.splice(2,3) //意思是从下标为2的位置删除3个元素得到 arr = [1,2,6]
//arr.splice()
```

6) 用splice修改或添加中间元素

```javascript
let arr = [1,2,3,4,5,6]
arr.splice(2,1,222) //意思是从下标为2的位置删除一个元素，并添加一个222,得到
//arr = [1,2,222,4,5,6]
arr.splice(2,1,222,333)//意思是从下标为2的位置删除一个元素，并添加222和333，得到
//arr = [1,2,222,333,4,5,6]
```

#### 5.2 遍历操作

1) 属性keys查看(不推荐)

```javascript
let arr = [1,2,3,4,5,6]
Object.keys(arr) //查看arr数组的所有属性名
Object.values(arr) //查看那arr数组的所有属性值
```

2) 对象属性in查看(不推荐)

```javascript
let arr = [1,2,3,4,5,6]
for(let i in arr){
    console.log(i)
}
```

3) for循环查看

```javascript
let arr = [1,2,3,4,5,6]
for(let i = 0; i < arr.length; i++){
    console.log(arr[i])
}
```

4) forEach遍历查看(数组的API)

```javascript
let arr = [1,2,3,4,5,6]
arr.forEach(function(item,index){
    console.log(item);
    console.log(index);
}) //item是数组内容，index是数组下标

//forEach接口的实现
function forEach(array, fn){
    for(let i = 0; i < array.lenght; i++){
        fn(array[i],i,array)
    }
}
```

for循环和forEach遍历的区别：

for循环中可以使用break和continue停止，但forEach不行。

5) indexOf查看元素是否在数组中

```javascript
let arr = [1,2,3,4,5,6]
arr.indexOf(22) //返回-1,说明22不在数组中
arr.indexOf(6)  //返回5，说明6在数组中，且下标为5
```

6) find函数是否查找到

```javascript
let arr = [1,2,3,4,5,6]
arr.find(function(x){
    return x%5 == 0
}) //find里面是函数，只要里面是真就返回符合条件的第一个值

//以上只能返回找到符合要求的值，若想返回符合条件值所在的下标，如下：
arr.findIndex(function(x){
    return x%5 == 0
})
```

#### 5.3 增加操作

1) 尾部添加元素

```javascript
let arr = [1,2,3,4,5,6]
arr.push(7)
arr.push(8,9,'10')
```

2) 头部添加元素

```javascript
let arr = [1,2,3,4,5,6]
arr.unshift(7) //得到arr = [7,1,2,3,4,5,6]
arr.unshift(8,9,10) //得到arr = [8,9,10,7,1,2,3,4,5,6]
```

3) 中间添加元素

```javascript
let arr = [1,2,3,4,5,6]
arr.splice(3,0,3.5) //在下标为3的位置不删除元素，添加一个3.5得到 arr = [1,2,3,3.5,4,5,6]
```

#### 5.4 其他操作

1) 反转操作

数组可以进行反转操作，倒置排序

```javascript
let arr = [1,2,3,4,5,6]
arr.reverse() //得到 arr=[6,5,4,3,2,1]，修改原来数组

//利用数组的reverse可以操作字符串反转问题，如下所示：
let str = 'abcde'
let arr = str.splice('')
arr.reverse()
str = arr.join('') //得到arr = 'edcba'

//或直接写为
str = str.splice('').reverse().join('')
```

2) 排序

```javascript
let arr = [2,5,1,3,4,6]
arr.sort() //得到数组从小到大的排序 arr=[1,2,3,4,5,6]

//JS默认是小的放前面，但是到底谁小它不知道，它也不知道要比谁，我们可以定义数值大的是小的，则就是从数值大的到小排序了。若想自定义是从大到小还是从小到大，如下：

//从小到大排序
arr.sort(function(a,b){
    if(a > b)
       return 1(or正值) //意思是谁值大就是大的
    else if(a == b){
        return 0 
    }
    else{
        return -1(or负值)  
    }
    // return a-b //简写形式
})
//从大到小排序：
arr.sort(function(a,b){
   if(a > b)
       return -1(or正值) //意思是谁值大就是小的
    else if(a == b){
        return 0  
    }
    else{
        return 1(or负值)  
    }
    // return b-a //简写形式
})
```

## 6. 数组的变换

以下变换都是不会改变原来数组，是返回执行该变换操作后形成的新数组

#### 6.1 map(n->n)

map是表示一一映射关系，参数为函数，一项项操作后返回，如想把数组中的每一项变成平方，如下：

```javascript
let arr = [2,5,1,3,4,6]

arr = arr.map(function(item){
      return item*item
}) //这是详写

arr = arr.map(item => item*item) //这是简写
```

#### 6.2 filter(n->少)

filter是对array进行一个过滤的操作，参数也为函数，一项项判断后返回真和假，真就要这个元素，返回假就舍弃这个函数。如想获得数组中的偶数，如下：

```javascript
let arr = [2,5,1,3,4,6]

arr = arr.filter(function(item){
    return item%2==0? true: false
}) //这是详写

arr = arr.filter(item => item%2==0? true: false) //这是简写
arr = arr.filter(item => item%2==0) //简写中的简写
```

#### 6.3 reduce(n->1)(强大且重要)

reduce是这一次会用到上一次的值，形参第一个是函数，第二个是变化的值的初始值，如下为求和实例：

```javascript
let arr = [2,5,1,3,4,6]

arr.reduce(function(sum, item){
    return sum += item
},0) //这是详写 sum初始值为0

arr.reduce((sum,item)=>{return sum += item},0) //这是简写
```

将map实现的数组元素全部平方用reduce方法实现为：

```javascript
let arr = [2,5,1,3,4,6]

arr.recuce((result, itme)=>{ return result.concat(item*item)},[])

//以上之所以要用concat连接的方法是因为想要返回一个数组，结果值result是个数组
```

将filter实现的过滤偶数的操作用reduce方法实现为：

```javascript
let arr = [2,5,1,3,4,6]

arr.reduce((result, item)=>{
    if(item %2 == 1){
        return result
    }  
    else{
        return result.concat(item)
    }
},[]) //详写版

arr.reduce((result,item)=> result.concat(item % 2 == 1? []:item),[]) //这是简写
```



