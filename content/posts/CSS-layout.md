---
title: "CSS布局"
date: 2020-01-28T12:29:49+08:00
tags: ["CSS"]
categories: ["CSS"]
draft: false
---

## 前言

CSS页面布局方式有多种，这里介绍三种针对不同需求的布局方式，分别为float布局、flex布局、grid布局，每种布局属性的浏览器支持程度可通过[caniuse](https://caniuse.com/)网站进行查询，这三种布局的具体使用方式和区别如下：


## 1. float布局方式

#### 需求分析

float布局是专门用于兼容ie浏览器的一种布局，几乎所有浏览器都支持float，但是float布局其相比于其他布局方式有点复杂，所以用float布局一般是为了兼容ie浏览器和其旧版本，若不必兼容ie，可使用下列比较简单好用的布局方式，float布局具体使用方式如下：

#### float的常用三种取值

**float: none**：

float的浏览器默认值，即不自定义float属性值时，该属性值为none，意味着该元素没有脱离标准文档流。只要自定义设置了float的属性值为非none值，则该元素就脱离了标准文档流的流向，成为了浮动元素。

**float: left**：

设置float值为left时，首先意味着该元素脱离文档流成为了浮动元素，其次是该值含义是该元素必须浮动在其所在块级容器剩余可用空间的最左侧，即该元素被移出正常的文档流向，一直向左移动，直到碰到了所处容器剩余可用空间的最左端边框或者碰到了另外一个浮动元素。如下图的左浮动示例图所示：

![layout_pic01](/imgs/layout_pic01.JPG)

**float: right**：

同left值的变化类似，该值的含义是该元素必须浮动在其所在块级容器剩余可用空间的最右侧，脱离文档流后一直向右移动，直到碰到所在容器剩余可用空间的最右端边框或者碰到另外一个浮动元素。如下图的右浮动示例图所示：

![layout_pic02](/imgs/layout_pic02.JPG)

#### 脱离文档流后再归父元素管理

浮动元素脱离文档流后由于其流向不再符合正常文档流向，所以可能会出现一些布局交叉乱掉的情况，如下图所示，这些元素都有一个共同的父元素，父元素的边框为蓝色，如下图所示，只有非浮动元素在父元素中，浮动元素不被包含在父元素中，也就是说，脱离文档流的元素不再归其父元素管了。

![layout_pic03](/imgs/layout_pic03.JPG)

若想让浮动元素也归父元素管理，则只需在父元素中添加class="clearfix"的class属性，然后设置如下：

```css
.clearfix:after{
	content: '';
    display: block;
    clear: both;
}
```

设置后的效果如下图所示，可看出，浮动元素也归父元素管理了。

![layout_pic04](/imgs/layout_pic04.JPG)

#### 自定义float值后的一些变化

自定义float值后左浮、右浮成为浮动元素后，由于css属性的非正交性(即一个属性的改变会影响另外一个属性的改变，即非正交)，会改变一些属性，目前我知道的其改变的属性如下：

1) 改变了该元素的display属性值，若该元素的display属性值原本是inline或者inline-block，都会被改成了block值，成为块级元素。

2) block块级元素的属性中自己占据一行的特点被改变，不再是自己占据一行，而是根据其内容大小确定其宽度，当然也可自定义宽度，而且若不自定义宽度width，可能还会出一些问题，所以最好设置了float浮动后加上width属性值。

#### float布局的使用总结

1) 在子元素上加上float: left / right，和width属性。

2) 在父元素上加上.clearfix属性，并添加对应属性值。


## 2. flex布局方式

#### 需求分析

flex布局，又称弹性布局，是目前使用最广泛的布局方式，除了ie浏览器外，大多数浏览器和其新版本都支持。这里有个英文网站介绍flex布局介绍得很详细，可参考这个[css-tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/#flexbox-basics)网站。

#### 工作原理

flex布局采取容器(container)和项目(item)结合的方式进行布局，容器是父元素，项目是多个子元素，为父元素启用flex属性，就意味着要对该元素内的物体进行flex布局，以下便从容器(container)和项目(item)两个方面各自具有的属性进行介绍。

#### flex—container属性

**1) 让一个元素变成flex容器**

给父元素加一个class="container"的class属性名，然后设置如下即可变成一个容器：(一般容器父元素是块级元素或者内联块元素)

```css
.container{
    display: flex / inline-flex;
}
```

flex和inline-flex的区别：

这两个属性值对其里面的项目子元素的布局没有任何影响，是对具有该容器属性的父元素类型的一个定义，flex是块级元素，inline-flex是内联块元素。对父元素同级的周围的元素有影响。

**2) 主轴方向：flex-direction**

flex布局默认是元素一字排开，flex布局下的元素没有块级元素、内联元素之分，经测试，flex布局下容器里的所有元素的{display: block / inline; }属性都没有任何作用，div也不再默认独占一行，而是根据其内容定大小，span的width、height属性也都起作用，可自定义其大小。

主轴方向属性是flex-direction，是用来定义一字排开的元素的方向是横着还是竖着。属性值如下：

**row：**默认值，主轴方向为从左向右，即将元素正向横着排布，如下图所示：

![layout_pic05](/imgs/layout_pic05.JPG)

**row-reverse：**主轴方向为从右向左，即将元素逆向横着排布，如下图所示：

![layout_pic06](/imgs/layout_pic06.JPG)

补充：在主轴方向为横向时，可看到所有元素都被挤在了一行，哪怕该元素设置了宽度也不起作用，文字都被挤成了竖着的，那是因为flex布局下的元素默认是一字排开，不换行。所以可以通过设置{flex-wrap: wrap;}属性来设置其换行，默认值是nowrap不换行，加入该属性后的样子如下图，可看到根据元素的内容大小或宽度进行换行。

![layout_pic09](/imgs/layout_pic09.JPG)

**column：**主轴方向为从上往下，即将元素竖着正向排布，如下图所示：

![layout_pic07](/imgs/layout_pic07.JPG)

**column-reverse：**主轴方向为从下往上，即将元素竖着逆向排布，如下图所示：

![layout_pic08](/imgs/layout_pic08.JPG)

**3) 横向对齐：justify-content**

这个属性一般用于主轴方向为横向，且加入了自动换行属性的容器，自动换行后该行可能会出现一些空隙，如何处理这些空隙，让元素在有空隙的情况下以何种方式分布，正是justify-content属性所处理的。具体属性值如下：

**flex-start：**默认属性值，即每行所有元素向左边靠拢，如下图所示：

![layout_pic10](/imgs/layout_pic10.JPG)

**flex-end**：每行所有元素向右边靠拢，如下图所示：

![layout_pic11](/imgs/layout_pic11.JPG)

**center：**每行所有元素居中靠拢，如下图所示：

![layout_pic12](/imgs/layout_pic12.JPG)

**space-between：**每行元素在两边对齐，中间平分空隙，如下图所示：

![layout_pic13](/imgs/layout_pic13.JPG)

**space-around：**每行元素的左右两边均有同等大小的空隙，所以中间元素的两个空隙挨着时空隙要大些，如下图所示：

![layout_pic14](/imgs/layout_pic14.JPG)

**space-evenly：**空隙空间平均分，两边也有空隙，如下图所示：

![layout_pic15](/imgs/layout_pic15.JPG)

**4) 纵向对齐：align-content**

该属性用于主轴方向为横向，且容器的高度高于多行元素的总高度，即纵向方向有空隙时，如何对纵向方向的空隙进行划分的布局方式，具体属性值如下：

**stretch：**当子元素没有自定义高度时，该属性值起作用，会将元素的高度拉伸，填满整个高度，如下图所示：

![layout_pic20](/imgs/layout_pic20.JPG)

**flex-start：**同justify-content类似，如下图所示：

![layout_pic21](/imgs/layout_pic21.JPG)

**flex-end：**同justify-content类似，如下图所示：

![layout_pic22](/imgs/layout_pic22.JPG)

**center：**同justify-content类似，如下图所示：

![layout_pic23](/imgs/layout_pic23.JPG)

**space-between：**同justify-content类似，如下图所示：

![layout_pic24](/imgs/layout_pic24.JPG)

**space-around：**同justify-content类似，如下图所示：

![layout_pic25](/imgs/layout_pic25.JPG)

**space-evenly：**同justify-content类似，如下图所示：

![layout_pic26](/imgs/layout_pic26.JPG)

**5) 次轴对齐：align-items**

这个属性是用于主轴方向为横向，而且每一行的每个元素的高度不同的情况的样式设置。具体属性值如下：

**flex-start：**默认属性值，即每行所有元素顶部对齐，如下图所示：

![layout_pic17](/imgs/layout_pic17.JPG)

**flex-end：**即每行元素底部对齐，如下图所示：

![layout_pic18](/imgs/layout_pic18.JPG)

**center：**即每行元素中间对齐，如下图所示：

![layout_pic19](/imgs/layout_pic19.JPG)

**stretch：**

**baseline：**

#### flex—item属性





