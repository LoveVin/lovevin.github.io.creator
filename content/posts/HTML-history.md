---
title: "HTML发展概况"
date: 2020-01-27T22:22:26+08:00
tags: ["HTML发展"]
categories: ["HTML"]
draft: false
---

### 1.万维网和互联网

**互联网**——互联网是指我们整个网络系统的总称，自网络的出现就叫互联网，最初是指一个IP与一个IP通过网络发送消息传递信息，将人与人之间相互连接起来，因此叫互联网。  

**万维网**——万维网简称WWW(World-Wide-Web)，是指输入一个网址(URL)，以HTTP传输协议传输，返回一个网页的上网方式，是由万维网之父Tim-Berners-Lee（蒂姆·伯纳斯·李）发明的，返回的该网页页面是用HTML(Hypertext-Marked-Language)超文本标记语言编写的，通过浏览器识别并以网页形式展现给人们的。 


### 2.HTML标准制定者

HTML标准是由W3C，即 World-Wide-Web-Consortium(W3C)万维网联盟建立的，W3C的创立者是Tim-Berners-Lee（蒂姆·伯纳斯·李）


### 3.HTML5和H5

**HTML5**——html5是html超文本语言的进化版，在原有的html语言上加入了新的标签和新的标准，是一套新的web开发标准。  

**H5**——h5不是html5的简称，和html5完全没有关系。h5是中国人自己造的专有名词，就是指手机版本的网页页面，实现语法不一定要用html5。简单说做一个h5就是指做个手机页面。


### 4.HTML特殊语法

* `<!DOCTYPE html>` 是标明以下语法是html语法，DOCTYPE是文档类型的意思。  
* 标签有双闭合标签和单闭合标签之分。  
* 标签属性有两种，一种是赋值型，attr=xxx或attr='xxx'或attr="xxx"，当属性值中无特殊字符时，有引号、单引号、双引号都可以，有特殊字符时必须加引号。
* 注释语法：`<!-- -->`


### 5.HTML基本语句解释

```html
<!DOCTYPE html>//标记文档类型为html
<html lang="en">//文档使用语言，有en英文，和zh-CN中文
  <head>
    <meta charset="UTF-8" />//定义编码方式为UTF-8
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body></body>
</html>
```