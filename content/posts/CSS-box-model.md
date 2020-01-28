---
title: "CSS盒模型"
date: 2020-01-28T12:34:37+08:00
tags: ["CSS","盒模型"]
categories: ["CSS"]
draft: false
---

## 1. 是什么

css在为html元素设置样式时，将每一个html元素看作一个盒子，在css根据文档流标准为元素分配空间时是根据元素的盒子大小分配的，在任意一个网页上打开开发者工具，选择页面一个元素，都可看到如下的盒模型：

![box_pic01](/imgs/box_pic01.JPG)


## 2. 由外向内的内容组成

#### margin—外边距

如上图的盒模型所示的位置，margin是盒模型最外面一层的空间区域，可自定义设置上下左右大小，一般看不见，但确实存在，用于排布元素与其他元素的间隔距离。

#### border—边框

如上图的盒模型所示的位置，border是可以用设置{border: 1px solid red}样式看到的，也是盒模型的组成中唯一可以明显看到大小的一项，是视觉上可以看到的元素的大小。

#### padding—内边距

如上图的盒模型所示的位置，内边距padding和外边距一样也是看不到但真实存在的元素中的空间组成部分，用于设置元素的边界和内容content之间的距离。

#### content—内容

如上图的盒模型所示的位置，padding里面的部分是内容content，是元素里面的文字或者其他元素内容。其大小也是视觉上看不到的，若padding值为0时，内容大小是border内线围成的大小。


## 3. 盒模型分类

盒模型分为两种，一种是内容盒(content-box)，一种是边界盒(border-box)，两者的区别如下：

#### 1. content-box

conten-box，是浏览器设置的默认值，每个html元素浏览器默认设置看作是内容盒子，属性设置语句为{box-sizing: content-box;}，用法是，针对元素的width、height属性，设置的大小是设置的盒模型中的content部分的大小，设置元素的width: 200px ，得到的盒模型如下图所示，可知是content内容的宽度为200px。

![box_pic02](/imgs/box_pic02.JPG)

#### 2. border-box

通过设置元素的样式为{box-sizing: border-box;}，则可将元素设置为边界盒，则针对元素的width、height属性，设置的大小是设置的盒模型中的border外边框包含的所有里面的大小，设置元素的width: 200px ，得到的盒模型如下图所示，则200 = border(1+1)+padding(20+20)+content(158)，除去border和padding大小剩余的即为content大小。

![box_pic03](/imgs/box_pic03.JPG)

#### 3. 哪个好用些？

我觉得因人而异吧，我觉得border-box好用些，因为在盒模型的组成部分中，只有边界border可显示出来视觉上明显看到，使用边界盒可以看到使用width和height属性设置的元素大小。