---
title: js 设计模式
top: false
cover: false
toc: true
mathjax: true
date: 2020-10-28 16:13:31
password:
summary:
tags: '设计模式'
categories:
---

什么是设计模式？

软件设计工程中，通用的解决方案。

# 单例模式

定义：保证一个类仅有一个实例，并提供一个访问它的全局访问点。

方法：实现方式是先判断实例是否存在，如果存在则直接返回，如果不存在就创建之后再返回, 确保多次使用构造函数都返回一个实例 ===> 每次调用构造函数时，返回指向同一个对象的指针 ===> 缓存初次创建的变量对象



优点：

1. **可以用来划分命名空间，减少全局变量的数量。**
2. **使用单体模式可以使代码组织的更为一致，使代码容易阅读和维护。**
3. **可以被实例化，且实例化一次。**



# 工厂模式

# 发布订阅模式

# 装饰者模式

