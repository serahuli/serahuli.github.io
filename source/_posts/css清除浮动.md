---
title: css清除浮动
top: false
cover: false
toc: true
mathjax: true
date: 2020-03-10 09:37:35
password:
summary:
tags: 'css'
categories: '前端'
---

### 清除浮动

- 浮动float最开始出现的意义是为了让文字环绕图片而已，后来用于让块级元素并排展示

  > float 会导致该浮动元素的块级元素的父元素高度塌陷，所以需要清除浮动

- 清除浮动是指清除由于子元素浮动带来父元素高度塌陷的影响。

#### 清除浮动的方法

1. 在浮动元素同级最后增加一个冗余元素为其设置 `clear:both`

   `clear`的取值可以是：left、right、both

   - 清除左边浮动
   - 清除右边浮动
   - 左右浮动都不要

   ```javascript
   .clear{clear:both; height: 0; line-height: 0; font-size: 0}
   ```

2. 给父元素增加 

   ```javascript
   overflow: hidden;
   // 或者设置overflow: auto;只要overflow不为visible即可
   zoom: 1;	//解决浏览器兼容问题
   ```

3. :after 方法

   ```javascript
   .outer {
       zoom:1;
   }    /*==for IE6/7 Maxthon2==*/
   .outer :after {
       clear:both;
       content:'';
       display:table;
       width: 0;
       height: 0;
       visibility:hidden;
   }
   ```

   

####  块格式化上下文(BFC) 

-  块级格式化上下文是CSS可视化渲染的一部分。它是一块区域，规定了内部块盒的渲染方式，以及浮动相互之间的影响关系。 
   -  BFC是就像一道屏障，隔离出了BFC内部和外部，内部和外部区域的渲染相互之间不影响。BFC有自己的一套内部子元素渲染的规则，不影响外部渲染，也不受外部渲染影响。 
   -  BFC的区域不会和外部浮动盒子的外边距区域发生叠加。也就是说，外部任何浮动元素区域和BFC区域是泾渭分明的，不可能重叠。 
   -  BFC在计算高度的时候，内部浮动元素的高度也要计算在内。也就是说，即使BFC区域内只有一个浮动元素，BFC的高度也不会发生塌缩，高度是大于等于浮动元素的高度的。 
   -  HTML结构中，当构建BFC区域的元素紧接着一个浮动盒子时，即，是该浮动盒子的兄弟节点，BFC区域会首先尝试在浮动盒子的旁边渲染，但若宽度不够，就在浮动元素的下方渲染 