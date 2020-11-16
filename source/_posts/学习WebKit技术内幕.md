---
title: 学习WebKit技术内幕
top: false
cover: false
toc: true
mathjax: true
date: 2020-11-14 23:18:31
password:
summary:
tags:
categories:
---

# 浏览器与浏览器内核

## 浏览器

- Berners-Lee （W3C组织的理事），发明了世界上第一个浏览器（WorldWideWeb）

- Safari内核：WebKit

- 移动系统：苹果的iOS系统操作系统和Google的安卓系统---WebKit

- 浏览器的特性：

  > - 网络
  > - 资源管理
  > - 网页浏览
  > - 多页面管理
  > - 插件和扩展
  > - 账户与同步
  > - 安全机制：提供一个安全的浏览器环境，避免用户信息被非法窃取或者破坏
  > - 开发者工具
  >
  > ![浏览器支持的操作系统](浏览器支持的操作系统.png)

- HTML5 类别和包含的各种规范

  | 类别       | 具体规范                                                     |      |
  | ---------- | ------------------------------------------------------------ | ---- |
  | 离线       | Application cache、Local storage、Indexed DB 、在线/ 离线 事件 |      |
  | 存储       | Application cache、Local storage、Indexed DB等               |      |
  | 连接       | Web Sockets, Server-sent 事件                                |      |
  | 文件访问   | File API, File System , FileWriter, ProgressEvents           |      |
  | 语义       | 各种新元素，包括Media, structural, 国际化，Link relation , 属性，form类型， microdata 等方面 |      |
  | 音频和视频 | HTML5 Vidio, Web Audio, WebRTC, Vedio track等                |      |
  | 3D和图形   | Canvas 2D，3D CSS变换，WebGL, SVG等                          |      |
  | 展示       | CSS3 2D/3D 变换，转换 transition , WebFonts等                |      |
  | 性能       | Web Worker, HTTP caching 等                                  |      |
  | 其他       | 触控和鼠标 , Shadow DOM , CSS masking 等                     |      |

  

- HTTP是构建在 TCP/IP 之上的应用层协议，用于传输 HTML文本和所涉及的各种资源，包括图片和多媒体资源等。HTTPS是安全版的HTTP, 在HTTP之下加入SSL/TLS;

- 用户代理（User Agent）是个奇怪的东西，其作用是表明浏览器的身份，因此互联网的内容供应商能够知道发送请求的浏览器身份，浏览器能够支持什么样的功能。

  > 用户代理信息是指浏览器像网站服务器发送HTTP请求头时加入的。

## 浏览器内核及特性

- 渲染引擎（浏览器内核）：将页面变成可视化的图像结果。

- 渲染就是根据描述或者定义构建数学模型，通过模型生成图像的过程。浏览器的浏览引擎就是能够将 HTML/CSS/Javascript文本及其相应的资源文件转换成图像结果的模块。

![浏览器引擎作用](浏览器引擎作用.png)

- 主流渲染引擎：Trident(IE)， Gecko(火狐)，WebKit(chrome, Safari, 安卓浏览器)

- ![渲染引擎模块及其依赖的模块](渲染引擎模块及其依赖的模块.png)

  > 一个渲染引擎主要包括 HTML解释器、CSS解释器、布局和 JavaScript 引擎等
  >
  > - HTML解释器：解释 HTML 文本的解释器，主要作用是将 HTML文本解释成DOM（文档对象模型）树，DOM是一种文档的表示方法。
  > - CSS解释器：级联样式的解释器，他的作用是为DOM中的各个元素对象出样式信息，从而为计算最后网页的布局提供基础设施。
  > - 布局：在DOM创建之后，WebKit需要将其中的元素对象同样式信息结合起来，计算他们的大小位置等布局信息，形成一个能够表示这所有信息的内部表示模型。
  > - JavaScript引擎：使用 JavaScript 代码可以修改网页的内容，也能修改CSS的信息，JavaScript引擎能够解释JavaScript代码并通过DOM接口和CSSOM接口来修改网页内容和样式信息，从而改变渲染结果
  > - 绘图：使用图形库将布局计算之后的各个网页的节点绘制成图像结果。
  >
  > ![渲染过程](渲染过程.png)

# HTML 网页和结构

​		HTML网页是利用HTML语言编写的文档，是一种半结构化的数据表现方式。结构特征可以归纳为三种：树状结构、层次结构和框结构。

> 网络上的每个资源都是由URL标记的，是URI的一种实现。对于浏览器来说，区分两个资源是否相同的唯一标准就是它们的URI是否一致。

​		在HTML的语法中，`frameset` `frame` `iframe`可以用来在当前网页中嵌入新的框结构。

## WebKit 的网页渲染过程

浏览器的主要作用就是将用户输入的URL转变成可视化的图像 ===》网页的渲染过程

> 网页通常比我们的屏幕可视面积要大，当前可视区域，称为视图(viewport)。所以，浏览器在渲染网页的时候一般会加入滚动条，就用户体验来说，垂直方向滚动好于水平方向。

根据数据的流向，渲染过程分为三个阶段：

- 从网页的URL到构建完DOM树
- 从DOM树到构建完WebKit的绘图上下文
- 从绘图上下文到生成最终的图像

![URL至DOM](URL至DOM.png)

>  具体过程如下：
>
> 1. 当用户输入网页URL的时候，WebKit调用其资源加载器加载该URL对应的网页。
> 2. 加载器依赖网络模块建立连接，发送请求并接收答复。
> 3. WebKit接收到各种网页或者资源的数据，其中某些数据可能是同步或者异步获取的。
> 4. 网页被交给HTML解释器转变成一系列的词语（Token）;
> 5. 解释器根据词语构建节点（Node),形成 DOM树
> 6. 如果节点是 JavaScript代码，调用JavaScript引擎解释并且执行。
> 7. JavaScript代码可能会修改DOM树的结构
> 8. 如果节点需要加载其他资源，例如图片、CSS、视频，调用资源加载器来加载他们，但是他们是异步的，不会阻碍当前DOM树的继续创建，如果是 JavaScript 资源URL(没有标记异步方式)，则需要停止当前DOM树的构建，直到JavaScript资源加载并且被JavaScript执行后才继续DOM树的创建。
>
> 两个事件：
>
> - DOMContentLoaded(DOM构建完成)
> - onload(DOM构建完成并且所有资源都加载完毕)

# WebKit 架构和模块



