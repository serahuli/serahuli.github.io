---
title: babel怎么将ES6转换成ES5
top: false
cover: false
toc: true
mathjax: true
date: 2020-11-11 11:24:51
password:
summary:
tags:
categories:
---

babel将 ES6+ 转换成 ES5 的步骤主要分为3步：

1. Parser解析：ES6语法解析成 AST抽象语法树 ===》 babylon 插件
2. Transformer转换：将打散的AST通过配置好的 plugins与presets转换成新的AST语法 ===》 babel-transform插件 [ plugins与presets的配置在 .babelrc文件中完成]
3. 将新的 AST 语法树对象再生成浏览器都可以识别的 ES5 语法 ===》 babel-generator

