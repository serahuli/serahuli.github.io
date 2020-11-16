---
title: BOM 学习
top: false
cover: false
toc: true
mathjax: true
date: 2020-10-30 21:05:32
password:
summary:
tags: 'javascript'
categories:
---

​		BOM是什么？BOM：浏览器对象模型，BOM提供了很多对象，用于访问浏览器的功能。

---

## window 对象

### 全局作用域

​		BOM 的 核心对象是 window, 表示浏览器的一个实例。在浏览器中， window既代表了JavaScript访问浏览器窗口的一个接口， 又是 ECMAScript规定的 global对象。 所以window是网页的全局变量。

```js
var globalV = '我是全局变量'
function getGlobalV() {
  console.log(this.globalV)
}

console.log(globalV) // 我是全局变量
console.log(window.globalV)  // 我是全局变量
getGlobalV()  // 我是全局变量
this.getGlobalV()  // 我是全局变量
window.getGlobalV()  // 我是全局变量
```

​		通过 var 声明的全局变量的数据属性[[ Configurable ]] 为 false, 所以直接通过 var 添加的 window属性是不可被删除（delete）的。

```js
var globalV = '我是全局变量';

window.windowV = '我是 window 创建的变量'

console.log(windowV) // 我是 window 创建的变量

delete window.globalV;
delete window.windowV;

console.log(globalV) // 我是全局变量
console.log(windowV) // error: Uncaught ReferenceError: windowV is not defined
```

​		删除之后：windowV 相当于未声明，所以会报错，如果你要想知道可能没有声明的变量是否存在，可以使用 window.[key] 进行查询(属性查询)

```js
var globalV = '我是全局变量';

window.windowV = '我是 window 创建的变量'

console.log(windowV) // 我是 window 创建的变量

delete window.globalV;
delete window.windowV;

console.log(globalV) // 我是全局变量
if(window.windowV) {
  console.log(windowV) // 不执行这个条件
}
```

