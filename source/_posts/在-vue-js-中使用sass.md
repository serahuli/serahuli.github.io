---
title: 在 vue.js 中使用sass
top: false
cover: false
toc: true
mathjax: true
date: 2019-9-20 09:36:59
password:
summary:
tags: 'vue'
categories: '前端'
---

- `npm install vue-loader --save-dev`

- `npm install node-sass --save-dev`

- `npm install sass-loader --save-dev`

- `npm install style-loader --save-dev`

- 安装完上述插件之后，就可以进行引用了

  ```scss
  <style lang="scss" scoped>
    $testColor: #f00;
  </style>
  ```

> 如果源码出现以下错误：则说明sass版本过高，只需要调为较低版本即可。实证有效版本：7.3.1
>
> - 修改之后删除`node_modules`文件夹
> - 然后`npm install` 重新下载
> - `npm run dev`即可
>
> ***TypeError: this.getResolve is not a function*** 