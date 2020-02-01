---
title: "JS的奇葩之处"
date: 2020-02-01T21:50:47+08:00
tags: ["JS奇葩"]
categories: ["JavaScript"]
draft: false
---

## 1. let房里房外

有以下两个代码，看似没区别，但结果天差地别，其中setTimeout时间间隔为0时表示尽快执行该代码，尽快那也得等到语句从头到尾执行完再执行了。

```javascript
let i;
for(i = 0; i < 6; i++){
    setTimeout(()=>{
        console.log(i);
    },0)
} //打印出6个6
```

```javascript
for(let i = 0; i < 6; i++){
    setTimeout(()=>{
        console.log(i);
    },0)
} //打印出0,1,2,3,4,5，因为每次循环都复制了一个i，实际一共7个i了
```

这样是不是使用setTimeout打印出0,1,2,3,4,5就没意义了，不如直接打印i，如下：

```javascript
let i;
for(i = 0; i < 6; i++){
     console.log(i);
} 
```

