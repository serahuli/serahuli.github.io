---
title: 微任务，宏任务，EventLoop
top: false
cover: false
toc: true
mathjax: true
date: 2020-10-29 16:03:08
password:
summary:
tags:
categories:
---

https://juejin.im/post/6844903914085564423

# 彻底搞懂 EventLoop

## EventLoop是什么？

EventLoop是一种定义的执行模式规范，浏览器与Node实现了不同的EventLoop。

## 相关定义：宏任务与微任务

宏任务:	**macrotask**, **tasks**, 属于宏任务的异步任务的回调会进入 macro task queue， 等本轮执行完毕之后执行。

> - setTimeout
> - setInterval
> - setImmediate (Node独有)
> - requestAnimationFrame (浏览器独有)
> - I/O
> - UI rendering (浏览器独有)

微队列:	**microtask，也叫jobs** 另一些异步任务的回调会依次进入micro task queue

> - process.nextTick (Node独有)
> - Promise
> - Object.observe
> - MutationObserver

**浏览器：**

先执行主线程 -》 再执行微任务 -》最后执行宏任务。如果在执行微任务或者宏任务的时候遇到另一个微任务，则添加到微任务队列后面，执行完本次任务即刻执行新添加的任务。

**Node**

先执行主线程 -》 再执行微任务 -》最后执行宏任务。如果在执行微任务或者宏任务的时候遇到另一个微任务，则添加到微任务队列后面，执行完本轮任务才可以进行下一轮任务。

**例题1**

```js
console.log(1);
console.log(2);
console.log(3);

//执行结果：1 -> 2 -> 3
```

**例题2**

```js
console.log(1);

setTimeout(function () {
  console.log(2);
}, 0);

console.log(3);

// 执行结果：1 -> 3 -> 2
```

**例题3**

```js
console.log(1);

const p = new Promise(function(resolve, reject) {
  console.log(2);
  resolve();
});

console.log(3);

setTimeout(function() {
  console.log(4);
}, 0);

p.then(function() {
  console.log(5);
  Promise.resolve().then(function() {
    console.log(6);
  })
})

setTimeout(function() {
  console.log(7);
})

console.log(8);

// 1 2 3 8 5 6 4 7
```

**例题4**

```js
setTimeout(function(){
  console.log('timeout1');
})

new Promise(function(resolve){

  console.log('promise1');
  for(var i =0; i <1000; i++) {
    i ==99&& resolve();
  }
  console.log('promise2');
}).then(function(){
  console.log('then1');
})

console.log('global1')

// promise1 -> promise2 -> global1 -> then1 -> timeout1

```

**例题5**

```js
console.log(1)

const p = new Promise(function(resolve, reject) {
  console.log(2)
  resolve()
});

console.log(3)
setTimeout(function() {
  console.log(4);
})

p.then(function() {
  console.log(5)
})

setTimeout(function() {
  console.log(6);
})

console.log(7)

// 1 2 3 7 5 4 6
```

**例题6**

```js
console.log('1');
async function async1() {
    console.log('2');
    await async2();
    console.log('3');
}
async function async2() {
    console.log('4');
}

process.nextTick(function() {
  console.log('5');
})

setTimeout(function() {
    console.log('6');
    process.nextTick(function() {
        console.log('7');
    })
    new Promise(function(resolve) {
        console.log('8');
        resolve();
    }).then(function() {
        console.log('9')
    })
})

async1();

new Promise(function(resolve) {
    console.log('10');
    resolve();
}).then(function() {
    console.log('11');
});

console.log('12');

// 1 2 4 10 12 5 11 3 6 8 7 9
```

注意点：

1. 新的微任务是添加到微任务队列的最后，浏览器环境本次执行，Node环境按轮次执行。
2. async 与 promise 本身是同步的。
3. promise的回调then, catch是异步的。
4. async返回值是 promise, await async2会先将结果添加到微任务队列。

例题6

```js
async function a1 () {
    console.log('a1 start')
    await a2()
    console.log('a1 end')
}
async function a2 () {
    console.log('a2')
}
console.log('script start')
setTimeout(() => {
    console.log('setTimeout')
}, 0)
Promise.resolve().then(() => {
    console.log('promise1')
})
a1()
let promise2 = new Promise((resolve) => {
    resolve('promise2.then')
    console.log('promise2')
})
promise2.then((res) => {
    console.log(res)
    Promise.resolve().then(() => {
        console.log('promise3')
    })
})
console.log('script end')
// script start -> a1 start -> a2 -> promise2 -> script end -> promise1 -> a1 end -> promise2.then -> promise3 -> setTimeout
```

