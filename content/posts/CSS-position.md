---
title: "CSS定位之position属性"
date: 2020-02-04T22:41:14+08:00
tags: ["position"]
categories: ["CSS"]
draft: false
---

## 前言

css中对html元素的管理是基于分层的管理，整个页面看起来是一个平面，实际是由浏览器解析每一层的元素布局和多层元素间的定位关系后汇总渲染成一个平面图片后展示出来的。

布局和定位是css中两个重要的知识点，二者是针对完全不同的方面。

**布局**：是管理同一层元素间的布局方式

**定位**：是管理元素所在层级的定位方式

## 非定位元素

#### position: static

非定位元素是指position值未曾修改，是默认的static值的元素。

该类元素待在文档流中，并遵循文档流布局方式。此时 `top`, `right`, `bottom`, `left` 和 `z-index `属性无效。

## 定位元素

定位元素的位置偏移属性是`top、bottom、left、right`，结合使用。

#### 1. 相对定位元素

#### position: relative

**相对于自身定位**

该类元素在正常文档流中原本所占的位置仍会以预留空间的方式存在，元素被放置在定位元素层，并可通过`top`, `right`, `bottom`, `left` 的方式设置元素相对于自身在正常文档流中原本的位置偏移。

若不设置偏移值，元素在视觉上的位置不变，只是所在层变了。可以配合absolute绝对定位元素使用，作为absolute绝对定位元素参考的父元素。

#### 2. 绝对定位元素

**绝对定位元素一般必须配合`设置top、bottom、left、right`中的上下、左右中各一个属性的值才可正常显示，否则有的浏览器会出错。**

#### 2.1 position: absolute

**相对于祖先元素中第一个定位元素定位（即position值不是static默认值的元素）**

该类元素会被完全移出正常文档流，并不为元素预留空间。该元素的`top`, `right`, `bottom`, `left` 值的参考是其祖先元素中第一个定位元素，如 top: 0; left: 0; 则元素是在其参考元素的左上角位置。

一般配合设置参考定位元素为的position值为relative使用。

**要善用left: 100%或50%，和负margin。**

**用途举例1：**

```css
//用于关闭按钮的定位
.div{
  border: 1px solid red;
  height: 200px;
  width: 200px;
    
  position: relative;
}
.close{
  border: 1px solid blue;
  width: 30px;
  height: 30px;
  text-align: center;
    
  position: absolute;
  top: 0;
  right: 0;
}
```

![position_pic01](/imgs/position_pic01.JPG)

**用途举例2：**

```html
<button>
      <span>这是个按钮上的鼠标悬浮提示</span>
      点击这里
</button>
```

```css
button{
  position: relative;
}
button span{
  border: 1px solid red;
  white-space: nowrap; //文字不换行
  position: absolute;
  bottom: calc(100% + 10px);
  left: 50%;
  transform: translateX(-50%);
  display: none;
}
button:hover span{
  display:inline-block;
}
```

![position_pic02](/imgs/position_pic02.JPG)

#### 2.2 position: fixed（移动端手机页面不要用，bug多）

**相对于屏幕视口定位**

该类元素会被移出正常文档流，并不为元素预留空间，而是通过指定元素相对于屏幕视口（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变。

当元素祖先的 `transform`, `perspective` 或 `filter` 属性非 `none` 时，容器由视口改为该祖先。该种情况会出错，因此不要将该元素放在有以上属性的元素里。

#### 3. 粘性定位元素

#### position: sticky（兼容性差）

**粘性定位可被认为是相对定位和固定定位的混合。元素在跨越特定阈值前为相对定位，之后为固定定位**

元素根据正常文档流进行定位，当其滚动祖先滚动到该元素位置时，会黏贴在固定偏移位置。

须指定` top`, `right`, `bottom`, `left` 四个阈值其中之一，才可使粘性定位生效。否则其行为与相对定位相同。

注意，一个sticky元素会“固定”在离它最近的一个拥有“滚动机制”的祖先上（当该祖先的`overflow` 是 `hidden`, `scroll`, `auto`, 或 `overlay`时），即便这个祖先不是真的滚动祖先。这个阻止了所有“sticky”行为

```css
position: -webkit-sticky;
position: sticky;
```

