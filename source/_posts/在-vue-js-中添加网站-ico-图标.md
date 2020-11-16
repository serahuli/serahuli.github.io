---
title: 在 vue.js 中添加网站 ico 图标
top: false
cover: false
toc: true
mathjax: true
date: 2020-10-27 09:31:11
password:
summary:
tags: 'vue'
categories: '前端'
---

> 准备：添加 `ico`图标在与`index.html`同级的目录

1. 第一种方法：

   在`index.html`中引入：

   ```html
   <link rel="shortcuticon" type="image/x-icon" href="./favicon.ico" /> 
   ```

2. 第二种方法

   在`webpack.dev.conf.js` 和 `webpack.prop.conf.js` 目录找到`plugins`的`new HtmlWebpackPlugin`中添加

   `favicon: './favicon.ico'`

   效果如下：

   ```javascript
   new HtmlWebpackPlugin({
         filename: 'index.html',
         template: 'index.html',
         inject: true,
         favicon: './favicon.ico'
       }),
   ```
   >  第二种方法的基础上还是无法显示，可以在`webpack.prod.conf.js`的相同位置添加``favicon: './favicon.ico'``

   3 . 一般两种方法择其一就好，修改配置之后要重新run 一下，查看网页源代码有配置ico的代码就对了；如果一直不对的话，清缓存

   	重启电脑就好；