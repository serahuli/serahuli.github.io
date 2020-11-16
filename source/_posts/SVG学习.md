---
title: SVG学习
top: false
cover: false
toc: true
mathjax: true
date: 2020-11-16 15:24:03
password:
summary:
tags:
categories:
---

---

# SVG

## hello svg

```html
<svg version="1.1" baseProfile="full" width="300" height="200" xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="red" />
  <circle cx="150" cy="100" r="80" fill="green" />
  <text x="150" y="125" font-size="60" text-anchor="middle" fill="white">SVG</text>
</svg>
```

> SVG 2之前，version属性和baseProfile属性用来供其他类型的验证识别SVG的版本。SVG 2不推荐使用version和baseProfile这两个属性。

> 作为XML的一种方言，SVG必须正确的绑定命名空间 （在xmlns属性中绑定）


> 元素的渲染顺序。SVG文件全局有效的规则是“后来居上”，越后面的元素越可见。

## 简介

### What ? 

- SVG 指可伸缩矢量图形 (Scalable Vector Graphics)
- SVG 用来定义用于网络的基于矢量的图形
- SVG 使用 XML 格式定义图形
- SVG 图像在放大或改变尺寸的情况下其图形质量不会有所损失
- SVG 是万维网联盟的标准
- SVG 与诸如 DOM 和 XSL 之类的 W3C 标准是一个整体

###  Why ? 

- SVG 可被非常多的工具读取和修改（比如记事本）
- SVG 与 JPEG 和 GIF 图像比起来，尺寸更小，且可压缩性更强。
- SVG 是可伸缩的
- SVG 图像可在任何的分辨率下被高质量地打印
- SVG 可在图像质量不下降的情况下被放大
- SVG 图像中的文本是可选的，同时也是可搜索的（很适合制作地图）
- SVG 可以与 Java 技术一起运行
- SVG 是开放的标准
- SVG 文件是纯粹的 XML

---

缺点：加载慢

### SVG 实例


```html
<!--声明， standalone="no"指包含一个外部文件的引用，该文件引用“http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd”-->
<?xml version="1.0" standalone="no"?>

<!--引用了这个外部的 SVG DTD。该 DTD 位于 "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd"。该 DTD 位于 W3C，含有所有允许的 SVG 元素。-->
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN"
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<!--SVG 代码以 <svg> 元素开始，包括开启标签 <svg> 和关闭标签 </svg> 。这是根元素。-->
<!--width 和 height 属性可设置此 SVG 文档的宽度和高度。-->
<!--version 属性可定义所使用的 SVG 版本，xmlns 属性可定义 SVG 命名空间。-->
<!--关闭标签的作用是关闭 SVG 元素和文档本身-->
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <circle cx="100" cy="50" r="40" stroke="black"
  stroke-width="2" fill="red" />
</svg>
```

### SVG 在 HTML 页面

SVG 文件可通过以下标签嵌入 HTML 文档：<embed>、<object> 或者 <iframe>

**使用 <embed> 标签**

- 优势：所有主要浏览器都支持，并允许使用脚本
- 缺点：不推荐在HTML4和XHTML中使用（但在HTML5允许）


```html
<embed src="circle1.svg" type="image/svg+xml" />
```

**使用 <object> 标签**

- 优势：所有主要浏览器都支持，并支持HTML4，XHTML和HTML5标准
- 缺点：不允许使用脚本。

```html
<object data="circle1.svg" type="image/svg+xml"></object>
```

**使用 <iframe> 标签**

- 优势：所有主要浏览器都支持，并允许使用脚本
- 缺点：不推荐在HTML4和XHTML中使用（但在HTML5允许）

```html
<iframe src="circle1.svg"></iframe>
```

**直接在HTML嵌入SVG代码**

> Firefox、Internet Explorer9、谷歌Chrome和Safari


```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
   <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red" />
</svg>
```

**链接到SVG文件**

```html
<a href="circle1.svg">View SVG file</a>
```

> 同样可以使用 img 元素，但是在低于4.0版本的Firefox 中不起作用

> SVG可以通过JavaScript动态创建并注入到HTML DOM中, 可以对浏览器使用替代技术，在不能解析SVG的情况下，可以替换创建的内容。

### 注意

1. SVG的元素和属性必须按标准格式书写，因为XML是区分大小写的（这一点和HTML不同）
2. SVG里的属性值必须用引号引起来，就算是数值也必须这样做。


### 文件类型

- `.SVG`
  - 普通SVG文件
  - HTTP头： 

```txt
Content-Type: image/svg+xml
Vary: Accept-Encoding
```

- `.svgz`
  - gzip压缩的SVG文件
  - HTTP头

```txt
Content-Type: image/svg+xml
Content-Encoding: gzip
Vary: Accept-Encoding
```

> 服务器配置错误是SVG加载失败的常见原因，所以一定要确保你的服务器配置正确。如果不能把服务器配置成给SVG文件发送正确的响应头，这时Firefox很有可能把该文件的标记显示成文本或乱码，甚至会要求查看者选择打开文件的应用程序。

---

## SVG网格

> 以页面的左上角为(0,0)坐标点，坐标以像素为单位，x轴正方向是向右，y轴正方向是向下。

![img](Canvas_default_grid.png)

### 像素?

> 基本上，在 SVG 文档中的1个像素对应输出设备（比如显示屏）上的1个像素。

- Scalable: 可缩放，缩放过后SVG 文档中的1个像素对应的不再是输出设备的1个像素

> SVG可以定义绝对大小(使用“pt”或“cm”标识维度),SVG也能使用相对大小，只需给出数字，不标明单位，输出时就会采用用户的单位。


```html
<svg width="200" height="200" viewBox="0 0 100 100">
```

- width and height: 定义了200*200的SVG画布
- viewBox: 画布可显示区域， 从（0， 0）开始到延伸到（100， 100）结束。

> viewBox（100*100）会放到（200*200）的SVG画布显示，形成放大两倍的效果

---

## SVG基本图形

- 矩形 <rect>
- 圆形 <circle>
- 椭圆 <ellipse>
- 线 <line>
- 折线 <polyline>
- 多边形 <polygon>
- 路径 <path>

### 矩形

```html
<rect x="60" y="10" rx="10" ry="10" width="30" height="30"/>
```

### 圆形

```html
<circle cx="25" cy="75" r="20"/>
```

### 椭圆

```html
<ellipse cx="75" cy="75" rx="20" ry="5"/>
```

### 线条

```html
<line x1="10" x2="50" y1="110" y2="150"/>
```

### 折线

```html
<polyline points="60 110, 65 120, 70 115, 75 130, 80 125, 85 140, 90 135, 95 150, 100 145"/>
```

### 多边形

> 终点自动折回起点

```html
<polygon points="50 160, 55 180, 70 180, 60 190, 65 205, 50 195, 35 205, 40 190, 30 180, 45 180"/>
```

### 路径

```html
<path d="M 20 230 Q 40 205, 50 230 T 90230"/>
```

---

## 路径

> path元素的形状是通过属性d定义的,属性d的值是一个“命令+参数”的序列

- 每一个命令都有两种表示方式，一种是用大写字母，表示采用绝对定位。另一种是用小写字母，表示采用相对定位（例如：从上一个点开始，向上移动10px，向左移动7px）。

> 属性d采用的是用户坐标系统，所以不需标明单位

- 绝对坐标大写， 相对坐标命令小写

### 直线

- 画点：`M x y`

- 画线：

  - `L x y`

  - `H x`
  - `V y`

- 闭合路径： `Z`


```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="200" height="100">
  <path d="M10 10 H 120 V 90 H 10 Z" fill="red" stroke="#ff0" />
  <path d="M10 10 h 110 v 80 h -110 Z" fill="yellow" stroke="pink" />
</svg>
```

---

### 曲线命令

#### 贝塞尔曲线

> 在path元素里，只存在两种贝塞尔曲线：三次贝塞尔曲线C，和二次贝塞尔曲线Q。

- 三次贝塞尔曲线需要定义一个点和两个控制点，所以用C命令创建三次贝塞尔曲线，需要设置三组坐标参数


```
C x1 y1, x2 y2, x y
```

控制点描述的是曲线起始点的斜率，曲线上各个点的斜率，是从起点斜率到终点斜率的渐变过程

```html
<?xml version="1.0" standalone="no"?>

<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg">

  <path d="M10 10 C 20 20, 40 20, 50 10" stroke="black" fill="transparent"/>
  <path d="M70 10 C 70 20, 120 20, 120 10" stroke="black" fill="transparent"/>
  <path d="M130 10 C 120 20, 180 20, 170 10" stroke="black" fill="transparent"/>
  <path d="M10 60 C 20 80, 40 80, 50 60" stroke="black" fill="transparent"/>
  <path d="M70 60 C 70 80, 110 80, 110 60" stroke="black" fill="transparent"/>
  <path d="M130 60 C 120 80, 180 80, 170 60" stroke="black" fill="transparent"/>
  <path d="M10 110 C 20 140, 40 140, 50 110" stroke="black" fill="transparent"/>
  <path d="M70 110 C 70 140, 110 140, 110 110" stroke="black" fill="transparent"/>
  <path d="M130 110 C 120 140, 180 140, 170 110" stroke="black" fill="transparent"/>

</svg>

```

![img](贝塞尔曲线1.png)

```
S x2 y2, x y
```

S命令可以用来创建与前面一样的贝塞尔曲线，但是，如果S命令跟在一个C或S命令后面，则它的第一个控制点会被假设成前一个命令曲线的第二个控制点的中心对称点。如果S命令单独使用，前面没有C或S命令，那当前点将作为第一个控制点。


```html
<?xml version="1.0" standalone="no"?>
<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M10 80 C 40 10, 65 10, 95 80 S 150 150, 180 80" stroke="black" fill="transparent"/>
</svg>
```

![image](贝塞尔曲线2.png)

- 二次贝塞尔曲线

```
 Q x1 y1, x y
```

```html
<?xml version="1.0" standalone="no"?>
<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M10 80 Q 95 10 180 80" stroke="black" fill="transparent"/>
</svg>
```

![image](贝塞尔曲线3.png)

```txt
T x y 
```

```html
<?xml version="1.0" standalone="no"?>
<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M10 80 Q 52.5 10, 95 80 T 180 80" stroke="black" fill="transparent"/>
</svg>
```

​															![image](贝塞尔曲线4.png)
​	快捷命令T会通过前一个控制点，推断出一个新的控制点。这意味着，在你的第一个控制点后面，可以只定义终点，就创建出一个相当复杂的曲线。需要注意的是，T命令前面必须是一个Q命令，或者是另一个T命令，才能达到这种效果。如果T单独使用，那么控制点就会被认为和终点是同一个点，所以画出来的将是一条直线。

#### 弧形曲线

> 弧形命令`A`是另一个创建SVG曲线的命令， 弧形可以视为圆形或椭圆形的一部分

> 根据半径和两点，可以画出四种弧形

```txt
 A rx ry x-axis-rotation large-arc-flag sweep-flag x y
 a rx ry x-axis-rotation large-arc-flag sweep-flag dx dy
```

```html
<?xml version="1.0" standalone="no"?>
<svg width="320px" height="320px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M10 315
           L 110 215
           A 30 50 0 0 1 162.55 162.45
           L 172.55 152.45
           A 30 50 -45 0 1 215.1 109.9
           L 315 10" stroke="black" fill="green" stroke-width="2" fill-opacity="0.5"/>
</svg>
```

![image-20200923115728306](SVG-弧形-参数解释.png)

```html
<?xml version="1.0" standalone="no"?>
<svg width="325px" height="325px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M80 80
           A 45 45, 0, 0, 0, 125 125
           L 125 80 Z" fill="green"/>
  <path d="M230 80
           A 45 45, 0, 1, 0, 275 125
           L 275 80 Z" fill="red"/>
  <path d="M80 230
           A 45 45, 0, 0, 1, 125 275
           L 125 230 Z" fill="purple"/>
  <path d="M230 230
           A 45 45, 0, 1, 1, 275 275
           L 275 230 Z" fill="blue"/>
</svg>
```

![image-20200923135702941](弧形2.png)

---

## Fill 和 stroke

- `fill`属性设置对象内部的颜色

- `stroke`属性设置绘制对象的线条的颜色。

- `fill-opacity`控制填充色的不透明度

- `stroke-opacity`控制描边的不透明度

- `stroke-width`控制描边的宽度

- `stroke-linecap`控制描边转角的样式，边框终点的形状

  ![img](描边样式.png)

- `stroke-linejoin`用来控制两条描边线段之间，用什么方式连接

  ![img](连接方式.png)

  ```html
  <polyline points="40 220 80 180 120 220" stroke="black" stroke-width="20"
        stroke-linecap="square" fill="none" stroke-linejoin="bevel"/>
  ```

- `stroke-dasharray`

  ![img](虚线.png)

  ```html
  <path d="M 10 75 Q 50 10 100 75 T 190 75" stroke="black"
      stroke-linecap="round" stroke-dasharray="5,10,5" fill="none"/>
  ```

- `fill-rule`定义如何给图形重叠的区域上色

- `stroke-miterlimit`定义什么情况下绘制或不绘制边框连接的`miter`效果；

- `stroke-dashoffset`定义虚线开始的位置

- 也可以通过CSS来样式化`填充`和`描边`(只有这两项)

  ```html
  <rect x="10" height="180" y="10" width="180" style="stroke: black; fill: red;"/>
  ```

- 利用`<style>`设置一段样式段落，可以重复使用

  ```html
  <?xml version="1.0" standalone="no"?>
  <svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" version="1.1">
    <defs>
      <style type="text/css"><![CDATA[
         #MyRect {
           stroke: black;
           fill: red;
         }
      ]]></style>
    </defs>
    <rect x="10" height="180" y="10" width="180" id="MyRect"/>
  </svg>
  ```

> 颜色名, rgb值, 十六进制值, rgba值

---

## 渐变

- 线性渐变
- 径向渐变

### 线性渐变

>  线性渐变沿着直线改变颜色，要插入一个线性渐变，你需要在SVG文件的`defs元素`内部，创建一个[`<linearGradient>`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element/linearGradient) 节点。

![img](线性渐变.png)

```html
<svg width="120" height="240" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <defs>
      <linearGradient id="Gradient1">
        <stop class="stop1" offset="0%"/>
        <stop class="stop2" offset="50%"/>
        <stop class="stop3" offset="100%"/>
      </linearGradient>
      <linearGradient id="Gradient2" x1="0" x2="0" y1="0" y2="1">
        <stop offset="0%" stop-color="red"/>
        <stop offset="50%" stop-color="black" stop-opacity="0"/>
        <stop offset="100%" stop-color="blue"/>
      </linearGradient>
      <style type="text/css"><![CDATA[
        #rect1 { fill: url(#Gradient1); }
        .stop1 { stop-color: red; }
        .stop2 { stop-color: black; stop-opacity: 0; }
        .stop3 { stop-color: blue; }
      ]]></style>
  </defs>
 
  <rect id="rect1" x="10" y="10" rx="15" ry="15" width="100" height="100"/>
  <rect x="10" y="120" rx="15" ry="15" width="100" height="100" fill="url(#Gradient2)"/>
  
</svg>
```

> `<linearGradient>`元素还需要一些其他的属性值，它们指定了渐变的大小和出现范围。渐变的方向可以通过两个点来控制，它们分别是属性x1、x2、y1和y2，这些属性定义了渐变路线走向。渐变色默认是水平方向的，但是通过修改这些属性，就可以旋转该方向。

### 径向渐变

> 径向渐变与线性渐变相似，只是它是从一个点开始发散绘制渐变。创建径向渐变需要在文档的`defs`中添加一个[`<radialGradient>`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element/radialGradient)元素

> 径向渐变也是通过两个点来定义其边缘位置，两点中的第一个点定义了渐变结束所围绕的圆环，它需要一个中心点，由`cx`和`cy`属性及半径r来定义，通过设置这些点我们可以移动渐变范围并改变它的大小

![img](径向渐变.png)

```html
<?xml version="1.0" standalone="no"?>
<svg width="120" height="240" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <defs>
      <radialGradient id="RadialGradient1">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
      <radialGradient id="RadialGradient2" cx="0.25" cy="0.25" r="0.25">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
  </defs>
 
  <rect x="10" y="10" rx="15" ry="15" width="100" height="100" fill="url(#RadialGradient1)"/> 
  <rect x="10" y="120" rx="15" ry="15" width="100" height="100" fill="url(#RadialGradient2)"/> 
  
</svg>
```

> 线性渐变和径向渐变都需要一些额外的属性用于描述渐变过程
>
> - `spreadMethod`:控制了当渐变到达终点的行为
>   - pad
>   - reflect
>   - repeat

```html
<?xml version="1.0" standalone="no"?>

<svg width="220" height="220" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <defs>
      <radialGradient id="GradientPad"
            cx="0.5" cy="0.5" r="0.4" fx="0.75" fy="0.75"
            spreadMethod="pad">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
      <radialGradient id="GradientRepeat"
            cx="0.5" cy="0.5" r="0.4" fx="0.75" fy="0.75"
            spreadMethod="repeat">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
      <radialGradient id="GradientReflect"
            cx="0.5" cy="0.5" r="0.4" fx="0.75" fy="0.75"
            spreadMethod="reflect">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
  </defs>

  <rect x="10" y="10" rx="15" ry="15" width="100" height="100" fill="url(#GradientPad)"/>
  <rect x="10" y="120" rx="15" ry="15" width="100" height="100" fill="url(#GradientRepeat)"/>
  <rect x="120" y="120" rx="15" ry="15" width="100" height="100" fill="url(#GradientReflect)"/>

  <text x="15" y="30" fill="white" font-family="sans-serif" font-size="12pt">Pad</text>
  <text x="15" y="140" fill="white" font-family="sans-serif" font-size="12pt">Repeat</text>
  <text x="125" y="140" fill="white" font-family="sans-serif" font-size="12pt">Reflect</text>

</svg>
```

![img](径向渐变终点行为示意图.png)

---

## 图案（patterns）

![img](图案.png)

```html
<?xml version="1.0" standalone="no"?>
<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <linearGradient id="Gradient1">
      <stop offset="5%" stop-color="white"/>
      <stop offset="95%" stop-color="blue"/>
    </linearGradient>
    <linearGradient id="Gradient2" x1="0" x2="0" y1="0" y2="1">
      <stop offset="5%" stop-color="red"/>
      <stop offset="95%" stop-color="orange"/>
    </linearGradient>

    <pattern id="Pattern" x="0" y="0" width=".25" height=".25">
      <rect x="0" y="0" width="50" height="50" fill="skyblue"/>
      <rect x="0" y="0" width="25" height="25" fill="url(#Gradient2)"/>
      <circle cx="25" cy="25" r="20" fill="url(#Gradient1)" fill-opacity="0.5"/>
    </pattern>

  </defs>

  <rect fill="url(#Pattern)" stroke="black" x="0" y="0" width="200" height="200"/>
</svg>	
```

---

## Texts

> 在SVG中有两种截然不同的文本模式. 一种是写在图像中的文本，另一种是SVG字体

```html
<text x="10" y="10">Hello World!</text>
```

- `text-anchor`: start、middle、end、inherit

- `font-family`

- `font-style`

- `font-weight`

- `font-variant`

- `font-stretch`

- `font-size`

- `font-size-adjust`

- `kerning`

- `letter-spacing`

- `word-spacing`

- `text-decoration`

- `tspan`: 该元素用来标记大块文本的子部分，它必须是一个`text`元素或别的`tspan`元素的子元素。一个典型的用法是把句子中的一个词变成粗体红色。

  ```html
  <text>
    <tspan font-weight="bold" fill="red">
      This is bold and red
    </tspan>
  </text>
  ```

  > **tspan属性**
  >
  > - x: 为容器设置一个新绝对`x`坐标,它覆盖了默认的当前的文本位置。这个属性可以包含一个数列，它们将一个一个地应用到`tspan`元素内的每一个字符上。
  >
  > - 从当前位置，用一个水平偏移开始绘制文本。这里，你可以提供一个值数列，可以应用到连续的字体，因此每次累积一个偏移。
  >
  > - y
  >
  > - dy
  >
  > - rotate: 把所有的字符旋转一个角度。如果是一个数列，则使每个字符旋转分别旋转到那个值，剩下的字符根据最后一个值旋转。
  >
  > - textLength: 给出字符串的计算长度。它意味着如果它自己的度量文字和长度不满足这个提供的值，则允许渲染引擎精细调整字型的位置。
  >
  > - tref: 允许引用已经定义的文本，高效地把它复制到当前位置。你可以使用`xlink:href`属性，把它指向一个元素，取得其文本内容
  >
  >   ```html
  >   <text id="example">
  >     This is an example text.
  >   </text>
  >   <text>
  >     <tref xlink:href="#example" />
  >   </text>
  >   ```
  >
  > - textPath: 该元素利用它的`xlink:href`属性取得一个任意路径，把字符对齐到路径，于是字体会环绕路径、顺着路径走。

---

## 基础变形

- g: `把属性赋给一整个元素集合`

  ```html
  <g fill="red">
    <rect x="0" y="0" width="10" height="10" />
    <rect x="20" y="0" width="10" height="10" />
  </g>
  ```

- transform： `变形`

- 平移：`第二个值默认为0` -> `translate()`

  ```html
  <rect x="0" y="0" width="10" height="10" transform="translate(30,40)" />
  ```

- 旋转：`第二个值默认为0` ->  `rotate()` -> `rotate()`的值是用角度数指定

  ```html
  <rect x="20" y="20" width="20" height="20" transform="rotate(45)" />
  ```

- 斜切：利用一个矩形制作一个斜菱形。可用`skewX()`变形和`skewY()`变形。每个需要一角度以确定元素斜切到多远。

- `scale()变形`改变了元素的尺寸。它需要两个数字，作为比率计算如何缩放。0.5表示收缩到50%。*如果第二个数字被忽略了，它默认等于第一个值。*

- ## 用`matrix()实现复杂变形`

  ![image-20200924100757786](martix复杂变形.png)

> 如果使用了变形，你会在元素内部建立了一个新的坐标系统，应用了这些变形，你为该元素和它的子元素指定的单位可能不是1:1像素映射。但是依然会根据这个变形进行歪曲、斜切、转换、缩放操作。
>
> ```html
> <g transform="scale(2)">
> <rect width="50" height="50" />
> </g>
> ```
>
> 比之HTML，SVG允许你无缝嵌入别的svg元素。因此你可以利用内部`svg`元素的属性`viewBox`、属性`width`和属性`height`简单创建一个新的坐标系统。
>
> ```html
> <svg xmlns="http://www.w3.org/2000/svg" version="1.1">
> <svg width="100" height="100" viewBox="0 0 50 50">
>  <rect width="50" height="50" />
> </svg>
> </svg> 
> ```
>
> 矩形将是指定的两倍大

---

## 剪切和遮罩

### 剪切

> **Clipping**用来移除在别处定义的元素的部分内容。在这里，任何半透明效果都是不行的。它只能要么显示要么不显示。
>
> **Masking**允许使用透明度和灰度值遮罩计算得的软边缘。

```html
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <clipPath id="cut-off-bottom">
      <rect x="0" y="0" width="200" height="100" />
    </clipPath>
  </defs>

  <circle cx="100" cy="100" r="100" clip-path="url(#cut-off-bottom)" />
</svg>
```

![img](clipdemo.png)

### 遮罩

> 遮罩的效果最令人印象深刻的是表现为一个渐变。如果你想要让一个元素淡出，你可以利用遮罩效果实现这一点。

```html
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <linearGradient id="Gradient">
      <stop offset="0" stop-color="white" stop-opacity="0" />
      <stop offset="1" stop-color="white" stop-opacity="1" />
    </linearGradient>
    <mask id="Mask">
      <rect x="0" y="0" width="200" height="200" fill="url(#Gradient)"  />
    </mask>
  </defs>

  <rect x="0" y="0" width="200" height="200" fill="green" />
  <rect x="0" y="0" width="200" height="200" fill="red" mask="url(#Mask)" />
</svg>
```

![img](maskdemo.png)

### opacity定义透明度

```html
<rect x="0" y="0" width="100" height="100" opacity=".5" />
```

- `fill-opacity`
- `stroke-opacity`

```html
<svg  width="200" height="200" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" >
  <rect x="0" y="0" width="200" height="200" fill="blue" />
  <circle cx="100" cy="100" r="50" stroke="yellow" stroke-width="40" stroke-opacity=".5" fill="red" />
</svg>
```

![img](opacitydemo.png)

---

## 其它SVG内容

### 嵌入光栅图像

> 很像在HTML中的`img`元素，SVG有一个`image`元素，用于同样的目的。你可以利用它嵌入任意光栅（以及矢量）图像。它的规格要求应用至少支持PNG、JPG和SVG格式文件。

```html
<svg version="1.1"
     xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
     width="200" height="200">
  <image x="90" y="-65" width="128" height="146" transform="rotate(45)"
     xlink:href="https://developer.mozilla.org/static/img/favicon144.png"/>
</svg>
```

![img](rotate-image-demo.png)

---

## 滤镜效果

> 滤镜通过 [`filter`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element/filter) 元素进行定义，并且置于 `<defs>` 区块中。在 `filter` 标签中提供一系列*图元*（**primitives**），以及在前一个基本变换操作上建立的另一个操作（比如添加模糊后又添加明亮效果）。如果要应用所创建的滤镜效果，只需要为 SVG 图形元素设置 `filter` 属性即可。

```html
<svg width="250" viewBox="0 0 200 85"
     xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <!-- Filter declaration -->
    <filter id="MyFilter" filterUnits="userSpaceOnUse"
            x="0" y="0"
            width="200" height="120">

      <!-- offsetBlur -->
      <feGaussianBlur in="SourceAlpha" stdDeviation="4" result="blur"/>
      <feOffset in="blur" dx="4" dy="4" result="offsetBlur"/>

      <!-- litPaint -->
      <feSpecularLighting in="blur" surfaceScale="5" specularConstant=".75" 
                          specularExponent="20" lighting-color="#bbbbbb"  
                          result="specOut">
        <fePointLight x="-5000" y="-10000" z="20000"/>
      </feSpecularLighting>
      <feComposite in="specOut" in2="SourceAlpha" operator="in" result="specOut"/>
      <feComposite in="SourceGraphic" in2="specOut" operator="arithmetic" 
                   k1="0" k2="1" k3="1" k4="0" result="litPaint"/>

      <!-- merge offsetBlur + litPaint -->
      <feMerge>
        <feMergeNode in="offsetBlur"/>
        <feMergeNode in="litPaint"/>
      </feMerge>
    </filter>
  </defs>

  <!-- Graphic elements -->
  <g filter="url(#MyFilter)">
      <path fill="none" stroke="#D90000" stroke-width="10" 
            d="M50,66 c-50,0 -50,-60 0,-60 h100 c50,0 50,60 0,60z" />
      <path fill="#D90000" 
            d="M60,56 c-30,0 -30,-40 0,-40 h80 c30,0 30,40 0,40z" />
      <g fill="#FFFFFF" stroke="black" font-size="45" font-family="Verdana" >
        <text x="52" y="52">SVG</text>
      </g>
  </g>
</svg>
```

![image-20200924143820025](lvjing.png)

---

### SVG 字体

> 定义一个SVG字体的基础是[`<font>`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element/font)元素。

![image-20200924145030529](../../../front_end_study/SVG/images/guifan.png)

---

## 其他

- 浏览器支持：Internet Explorer 9、Mozilla Firefox、Safari、Google Chrome和Opera。基于Webkit的移动设备浏览器（主要是指iOS和Android），都支持SVG。

- [Inkscape](http://www.inkscape.org/)

- [Adobe Illustrator](http://www.adobe.com/products/illustrator/)

- [Apache Batik](http://xmlgraphics.apache.org/batik/)

- [Google Docs](http://www.google.com/google-d-s/drawings/)

  > 从Google Docs绘制，可以被输出为SVG。

---

## 最后一点干货

！ 将`png`转成 `svg`

- https://www.aconvert.com/cn/image/png-to-svg/
- https://jinaconvert.com/cn/convert-to-svg.php
- https://blog.csdn.net/qq_32250025/article/details/79206631

