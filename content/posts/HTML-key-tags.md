---
title: "HTML重点标签篇"
date: 2020-01-28T12:15:01+08:00
tags: ["HTML重点标签"]
categories: ["HTML"]
draft: false
---

## 1. a 标签

**href 属性**：href即hyper(超级)-reference(链接/引用)的缩写，即为超链接的意思。该属性值为超链接地址名。该属性值的取值形式为：   

1）网络地址：
* "https://baidu.com"：
* "http://baidu.com"：
* "//baidu.com"：无协议网址  

2）文件路径：
* 相对路径：同一文件内的本地html页面所在的相对路径名作为链接地址。
* 绝对路径：当前打开的文件为根目录

3）伪协议：
* " javescript:代码; "：可用于写一个a标签但又不想做任何操作，就用href="javascript:;"。若用href=""，点击会刷新页面，href="#"点击不会刷新页面但是会跳转至顶部。因此，只有用js伪协议才能真正做到点击a标签什么都不做。
*  "#id值"：可跳转到该id值标签的内容所在部分。
* " mailto:邮箱 "：打开邮箱并自动填入邮箱地址
* " tel:手机号"：打开拨号页面并自动填入号码


**target 属性**：该属性是指跳转方向的意思，即将在哪个窗口打开该链接地址。基本属性值有五类，分别为

* "_self"：在当前页面打开超链接   
* "_blank"：在新的空白页面打开超链接  
* "_parent"：若有iframe包含的子窗口、孙窗口等，在当前窗口的上一层父窗口打开超链接  
* "_top"：若有iframe包含的子窗口、孙窗口等，在最外层窗口即祖宗窗口打开超链接。
* "xxx"：会先检查有没有叫xxx名字的窗口，若没有则新建一个窗口命名为xxx，当后面再有一个值为xxx时便是该窗口打开。可用于设置利用同一个窗口打开覆盖多个页面。也可给iframe窗口的name命名为xxx，则打开的页面就是在iframe窗口打开了。

**download 属性**：非赋值属性，开启后点击该链接会下载超链接地址中的网页，而不是查看，但浏览器大部分不支持。

## 2. table 标签
tabel中常用的结构标签有三个，分别是：
```
<table>
      <thead>表头</thead>
      <tbody>主体</tbody>
      <tfoot>表尾</tfoot>
    </table>
```
然后是表项标签分别有：
* tr：即table row，是表中的一行
* th：即table header，是指表头，默认会加粗显示。
* td：即table data：表中的一项数据

**table的几个样式**：
* table-layout：可用于定义每列宽度是相等还是根据字数大小分布。auto和fixed。
* border-collapse：取值为collapse，则可合并单元格去除表项内边界。
* border-spacing：一般设置边界间隔为0。 

## 3. img 标签
该标签会发出一个get请求，返回一张图片。

**属性**

**src 属性**：属性值为图片的地址，可为网络地址也可为相对或者绝对路径。  

**alt属性**：即alternative，可供选择的，当图片加载失败后，显示该部分内容。

**width**：只写宽度，高度会自适应等比缩放。

**height**：只写高度，宽度会自适应等比缩放。

**事件**

onload和onerror，其中onerror可用于加载图片加载失败的图片。

## 4. form 标签
该标签会发送一个get或者post请求然后刷新页面

**属性**

**action属性**：以get或者post的方式请求到action属性值里对应的页面。

**method属性**：请求方式的设置，get和post。

**autocomplete属性**：设置form的autocomplete属性值为"on"，然后在表单的input的输入标签中设置input的name="username"，则输入框获得焦点后会显示用户在该浏览器上曾经输入过的用户名。可选择并自动填充。

**target属性**：和a标签的target属性类型，设置提交到哪个页面。

**事件**

onsubmit事件

**from相关的其他知识**：

form中一定要有个type="submit"的提交按钮，可以是`<input type="submit"/>`也可以是`<button type="submit">提交</button>`，其中button不写类型默认是type="submit"。两个按钮的区别是，input标签里不能有其他内容，但button标签里可以再包含其他标签，也可用图片做按钮等。

## 5. input 标签
该标签的主要目的是让用户输入内容

**属性**：

**type 属性**：
* text：默认属性值，为输入文本框
* button：为按钮
* color：为一个颜色选择器
* password：为输入密码，不显示输入内容，以······代替
* radio：单选，要设置多个radio类型的input的name属性值相同，归为一组，在一组中单选
* checkbox：多选，一组checkbox类型的input也要name相同，便于后续获取该选择的数组。
* file：选择一个文件，在其后再加multiple即` <input type="file" multiple/>`，可同时选择多个文件内容。 
* hidden：隐藏文本框
* number：只能输入数字，且可从输入的数字连续点击增1减1。
* search：搜索框，会有x号出现删除搜索内容

**required 属性**：
非赋值属性，启用该属性则点击提交时提示请填写此字段，HTML自带的验证功能。

**事件**：
* onchange：内容改变时触发的事件
* onfocus：文本框获得焦点时触发的事件
* onblur：文本框失去焦点时触发的事件

## 6. textarea 标签
input是单行输入，textarea是多行输入，且什么属性不设置的话，该文本框可被拖动放大缩小。可设置其style属性为`<textarea style="resize: none;"></textarea>`可固定该文本框大小禁止拖动。

## 7. select+option 标签
可用于做选择列表，option标签是每一项内容。

未完待续。。。。