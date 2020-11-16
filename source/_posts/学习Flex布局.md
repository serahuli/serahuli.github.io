---
title: 学习Flex布局
top: false
cover: false
toc: true
mathjax: true
date: 2019-6-12 10:16:48
password:
summary:
tags: '前端'
categories: '前端'
---

# Flex布局

layout（布局）是 html + css 的重点应用

布局的传统解决方案，基于盒装模型：display + position + float

## Flex 布局基本概念

`Flexible Box`, 弹性布局, 是相当灵活的布局方式。

任何一种容器都可以指定 flex布局。Webkit 内核的浏览器，必须加上`-webkit`前缀

```js
.box {
  display: -webkit-flex; /* Safari */
  display: flex;
  
  /** 行内元素 */
  display: inline-flex;
}
```

**当设为 Flex布局之后，子元素的 `float`, `clear`, `vertical-align` 将会失效。**

**容器**：采用 Flex 布局的元素 => (flex container)，当一个元素成为容器之后，所有子元素都会成为 容器成员（flex item），也称为`项目`

![image-20201020141218865](image-20201020141218865.png)

容器存在两根轴，水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做`main start`，结束位置叫做`main end`；交叉轴的开始位置叫做`cross start`，结束位置叫做`cross end`。

**项目默认沿主轴排列**, 单个项目占据的主轴空间叫做`main size`，占据的交叉轴空间叫做`cross size`。

![img](bg2015071004.png)

## 容器相关属性

> - flex-direction
> - flex-wrap
> - flex-flow
> - justify-content
> - align-items
> - align-content

### flex-direction

`flex-direction`决定主轴的方向，也就是项目的排列部署方向，有四个值可选

> - `row`（默认值）：主轴为水平方向，起点在左端。
> - `row-reverse`：主轴为水平方向，起点在右端。
> - `column`：主轴为垂直方向，起点在上沿。
> - `column-reverse`：主轴为垂直方向，起点在下沿。

![image-20201020141840357](image-20201020141840357.png)

```css
.box {
  flex-direction: column | column-reverse | row | row-reverse;
}
```

### flex-wrap

`flex-wrap`属性定义，如果一条轴线排不下，如何换行, 默认在一行不换行，可选值有三个

```css
.box {
  /** 默认值，不换行 */
  flex-wrap: nowrap; 
  
  /** 换行，第一行在上方。 */
  flex-wrap: wrap; 
  
  /** 换行，第一行在下方 */
  flex-wrap: wrap-reverse;
}
```

### flex-flow

`flex-flow` 是 `flex-direction `与`flex-wrap`的简写，默认值为`row nowrap`, 先设置` flex-direction  `

### justify-content

`justify-content`属性定义了项目在主轴上的对齐方式，`flex-start`是默认值, 有五个值可选

> - flex-start: 左对齐(所有项目靠左，即时右边空余还很多)
> - flex-end： 右对齐
> - center: 居中
> - space-around: 两端对齐，项目之间的间隔都相等
> - space-between: 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍

![img](bg2015071010.png)

### align-items

`align-items`属性定义项目在交叉轴上如何对齐, `stretch`是默认值, 有五个值可选

> - flex-start: 交叉轴的起点对齐
> - flex-end: 交叉轴的终点对齐。
> - center: 交叉轴的中点对齐。
> - baseline: 项目的第一行文字的基线对齐。
> - stretch: 如果项目未设置高度或设为auto，将占满整个容器的高度。

![img](bg2015071011.png)

### align-content

`align-content`属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。`stretch`是默认值

> - flex-start：与交叉轴的起点对齐。
> - flex-end: 与交叉轴的终点对齐。
> - center: 与交叉轴的中点对齐。
> - space-between:  与交叉轴两端对齐，轴线之间的间隔平均分布。
> - space-around:  每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
> - stretch: 轴线占满整个交叉轴。

![img](bg2015071012.png)

---

## 项目相关属性

> - order:
> - flex-grow
> - flex-shrink
> - flex-basis
> - flex
> - align-self

### order

定义项目的排列顺序。数值越小，排列越靠前，默认为0，可以是正数或者负数

### flex-grow

`flex-grow`属性定义项目的放大比例，默认为`0`，即如果存在剩余空间，也不放大。

如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

![img](bg2015071014.png)

### flex-shrink

`flex-shrink`属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

如果所有项目的`flex-shrink`属性都为1，当空间不足时，都将等比例缩小。如果一个项目的`flex-shrink`属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效。

###  flex-basis

`flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小。

```js
.item {
  flex-basis: <length> | auto; /* default auto */
}
```

设为跟`width`或`height`属性一样的值（比如350px），则项目将占据固定空间。

### flex

`flex`属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选。

```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```

该属性有两个快捷值：`auto` (`1 1 auto`) 和 none (`0 0 auto`)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

### align-self

`align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。

> - auto
> - flex-start
> - flex-end
> - center
> - baseline
> - stretch

![img](bg2015071016.png)

