---
title: vue项目兼容IE浏览器
top: false
cover: false
toc: true
mathjax: true
date: 2020-10-27 09:39:32
password:
summary:
tags: 'css'
categories: '前端'
---

我使用 vue-cli 搭建的项目，chorm浏览器一切正常，但是IE浏览器却是一片空白，出现这种问题，是因为缺少 `babel-polyfill` 处理器的缘故;

1、安装 `babel-polyfill`
     ` npm install babel-polyfill --save-dev`
2、在`main.js`文件中引入`babel-polyfill`；
      `import 'babel-polyfill'`
3、在 webpack配置文件 `webpack.base.config.js` 中将entry中的app: './src/main.js'配置改为：app: ['babel-polyfill', './src/main.js']；
![](1879741-20200610212728544-2021199193.png)

--- 配置完之后重新打包刷新浏览器即可。



------------------2020.6.22更新
如果用到了第三方插件，即用到了 ‘babel-loader’解析的地方，也需要进行配置：
![](1879741-20200622120054186-240213618.png)