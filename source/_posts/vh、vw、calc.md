---
title: vh、vw、calc
top: false
cover: false
toc: true
mathjax: true
date: 2020-3-18 09:36:05
password:
summary:
tags: 'css'
categories: '前端'
---

### vh、vw

> `vh`与`vw` 是一个  js 与 css耦合的单位，经常用来做响应式布局,这两个单位是 css3引入的

视口是指：浏览器可视区域

- vw: 相对于视口的宽度。视口被均分为100单位的vw
- vh: 相对于视口的高度。视口被均分为100单位的vh
- vmax: 相对于视口的宽度或高度中较大的那个。其中最大的那个被均分为100单位的vmax
- vmin: 相对于视口的宽度或高度中较小的那个。其中最小的那个被均分为100单位的vmin

>所以 100vh是指整个视图窗口的高度。
>
>100vw是指整个视图窗口的宽度

### calc

- calc 是 css3 提供的在 css 中提供的计算值的函数

> - calc() 函数支持对 + 、- 、* 、/ 、运算
>
> - calc()函数使用标准的数学运算优先级规则 
> - 任何长度值都可以使用calc()函数进行计算 

**运算符前后都需要保留一个空格** ，否则calc不会生效

如： `calc(100vw - 10px)`

		`calc(100vmax - 10vh)`

> calc使用的兼容性

 ![img](https://img-blog.csdn.net/20161205142448327?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center) 