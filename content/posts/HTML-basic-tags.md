---
title: "HTML基本标签篇"
date: 2020-01-28T12:04:43+08:00
tags: ["HTML基本标签"]
categories: ["HTML"]
draft: false
---

### 1.结构标签   

html文件的基本结构为：
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head> </head>
<body> </body>
</html>
```
其中head标签部分一般放看不见的相关设置内容，页面显示的内容是在body中编写，在body标签中body被一些标签划分成有结构的部分。
```html
<body>
    <header>头部</header>
    <div>
        <main>页面主要部分</main>
        <aside>次要部分</aside>
    </div>
    <footer>尾部</footer>
  </body>
```
除此之外还有的结构标签有：   
**h1~h6**：加粗标题   

**section**：划分文档中的一个独立部分  ，一般包含一个h标题和一p段等。   

**article**：划分文档中的文章部分，一篇文章又可包含多个section部分。   

**p**：块级元素，表示文本的一个段落。  

**div**：是一个无实义容器标签，将文档分区。


### 2.内容标签

**ol+li**：ol即ordered list，li即list-item。该组合是编写有序列表内容的。ol标签为列表，li标签为列表项。ol中只能有li列表项，列表项中才能写内容 。  

**ul+li**：ul即unordered list，与ol相对应的无序列表。  

**dl+dt+dd**：dl即description-list描述列表，dt即description-term写描述的对象是谁，dd即description-data对该对象的描述内容

**pre**：html默认多个空格或tab或回车都显示为一个空格，添加pre标签包裹内容可以保留多个空格、tab、回车等样式。

**code**：code标签是用来包裹代码片段的，代码的字母一般是等宽的，如不加code，字母不等宽，代码不好看。用pre+code写代码片段。

**hr**：水平分割线

**br**：br即break，换行。

**em**：em即emphasis强调的意思，可用于强调一句话中的某个词，显示样式为斜体，样式可改。

**strong**：给一句话加上Strong表示该句是重点，显示样式为加粗，样式可改。

**quote**：内联引用，如果想换行用块行引用，即用blockquote标签


