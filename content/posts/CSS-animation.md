---
title: "CSS动画"
date: 2020-01-28T12:41:25+08:00
tags: ["CSS"]
categories: ["CSS"]
draft: false
---

## 1. 浏览器渲染原理

浏览器提供的所有功能中有一个非常重要的功能机制即渲染页面功能，使用渲染引擎实现，浏览器的渲染原理是不断擦掉重绘的过程，渲染过程如下：

**1) 根据HTML构建HTML树(DOM)**

 **2) 根据CSS构建CSS树(CSSDOM)**

**3) 将两棵树合成一棵渲染树(render tree)**

**4) layout确定布局定位**

**5) Paint绘制上色**

**6) 根据层叠上下文进行Composite合成**

在绘制完成后，可通过JS改变CSS样式，通过JS引擎与渲染引擎进行通信，告诉渲染引擎重新绘制页面，一般进行4、5、6过程，即layout、paint、composite，根据JS改变的情况确定重新渲染的步骤。可在该网站查看哪些属性触发哪些步骤[CSSTriggers](https://csstriggers.com/)

**关于浏览器渲染原理的三个推荐网站**

[推荐1](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction)

[推荐2](https://developers.google.com/web/fundamentals/performance/rendering/)

[推荐3](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count)


## 2. CSS性能问题

在开发者工具中，按下Esc键，出来新的控制台面板，再按Esc键取消。在...more tool中选择Rendering，勾选Paint Flashing，刷新页面，看到绿色的块快在闪，说明浏览器在重新渲染绘制页面。

在开发者工具中调试数据值时，鼠标光标放置在数字上，按上下可增1减1,按住shift键再按上下可增10减10

**1) 优化方法1**

运用translate平移，而不用left平移。


## 3. CSS之transform属性

transform即变形的意思，元素在该属性下，可进行平移、旋转、缩放等变形，具体变形方式如下：

### translate平移属性

**1) 常用属性值**

translateX：向X轴横轴方向平移，若平移的值为百分数，则表示的是移动本元素X轴方向长度的百分比数。

translateY：向Y轴纵轴方向平移

translateZ：向三维空间的Z轴方向平移，需要配合视图框和视点，在移动元素的父元素中的属性中确定视点距离屏幕的距离，视点的平面位置是父元素的正中心，Z轴值的变化是元素逐渐向视点靠近或远离的，如下图所示：

```css
.wrapper{
  perspective: 100px;//视点距离屏幕平面的距离
  border: 2px solid;
}
```

translate：X轴和Y轴方向的变化值

translate3d：X轴、Y轴和Z轴的变化值

**2) translate的巧用**

可结合绝对定位设置元素绝对居中，具体设置如下：

设置元素为绝对定位，设置其父元素为绝对定位（根据CSS定位的原理设置的，可参考CSS定位原理），然后在绝对定位设置left: 50%，top: 50%，此时元素的锚点所在位置即左上角点即在父元素正中心，再利用transform的百分数值平移，translateX(-50%)和translateY(-50%)，或者简写形式，如下图所示：

```css
父元素
.wrapper{
  border: 2px solid;
  height: 300px;
  position: relative;
}
定位子元素
#demo{
  border: 2px solid red;
  width: 100px;
  height: 100px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translateX(-50%) translateY(-50%);
  /*或transform: translate(-50%, -50%);*/
}
```

#### rotate旋转属性

**1)常用属性值**

rotate：默认绕着垂直于屏幕的Z轴旋转，值的单位为度，deg，如rotate(30deg)。

rotateX：绕着X轴旋转，要想象XYZ的立体空间。

rotateY：绕着Y轴旋转

rotateZ：默认旋转方向。

### scale缩放属性

**1) 常用属性值**

scale：X轴和Y轴同时缩放

scaleX：X轴缩放

scaleY：Y轴缩放

可配合transition: all 1s; 属性设置过渡缩放效果。

#### skew倾斜属性

skew、skewX、skewY，均尝试下可看到效果，取值单位也是度deg。

#### 总结

以上的transform属性可同时使用，直接空格隔开即可，不能写两个tranform，那样会覆盖的。


## 4. CSS之transition属性

transition即过渡的意思，该属性设置语句要加在要使用的元素本体上，功能是在元素的初始状态和结束状态之间添加过渡帧，使之过渡流畅。具体语法为：

transition: 属性名(all/其他) 时长(m/ms) 过渡方式 延迟(m/ms);

语法解读为：当该元素的该属性变化时，在设置的时长内，以该种过渡方式慢慢变化至末尾状态，若设置了延迟时间，则要等待延迟时间结束后执行该变化。

**过渡方式**：

linear：线性过渡

ease：非线性过渡

ease-in / ease-out / ease-in-out / cubic-bezier / step-star / step-end / steps

具体过渡函数的解释可看如下链接[mdn](https://developer.mozilla.org/zh-CN/docs/Web/CSS/timing-function)

**无法过渡的属性：**

1) display: block 到display: none，或者反过来，无法过渡


## 5. CSS之animation属性

**1) 定义关键帧**

```css
@keyframes 自定义动画名{
    0%{
        位置变化1
    }
    50%{
        位置变化2
    }
    100%{
        位置变化3
    }
}
```

**2) 调用帧动画**

animation: 时长 | 过渡方式 | 延迟时长 | 次数 | 方向 | 填充模式 | 是否暂停 动画名

动画名：是必须有的选项。

时长 / 延迟时长：以m秒和ms毫秒为单位

过渡方式：和transition的过渡方式一样

次数：数值，无数次是 infinite

方向：reverse、alternate、alternate-reverse。

填充模式：none、forwards、backwards、both。

是否暂停：paused、running。

每个对应属性都有自己的单独属性。





