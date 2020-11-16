---
title: css垂直居中
top: false
cover: false
toc: true
mathjax: true
date: 2019-12-21 17:20:03
password:
summary:
tags: 'css'
categories: 'css'
---

# CSS水平垂直居中

### 居中元素宽高已知

1. 子绝父相

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>Document</title>
     <style>
       * {
         margin: 0;
         padding: 0;
       }
       html, body {
         width: 100%;
         height: 100%;
       }
       body {
         position: relative;
       }
       .outer {
         width: 100px;
         height: 100px;
         background: pink;
   
         position: absolute;
         top: 50%;
         left: 50%;
         margin-top: -50px;
         margin-left: -50px;
       }
     </style>
   </head>
   <body>
     <div class="outer"></div>
   </body>
   </html>
   ```

2. position + margin:auto

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>Document</title>
     <style>
       * {
         margin: 0;
         padding: 0;
       }
       html, body {
         width: 100%;
         height: 100%;
       }
       body {
         position: relative;
       }
       .outer {
         width: 100px;
         height: 100px;
         background: pink;
   
         position: absolute;
         top: 0;
         left: 0;
         bottom: 0;
         right: 0;
         margin: auto;
       }
     </style>
   </head>
   <body>
     <div class="outer">
       <!-- <div class="inner"></div> -->
     </div>
   </body>
   </html>
   ```

   

3. position + calc

    ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>Document</title>
     <style>
       * {
         margin: 0;
         padding: 0;
       }
       html, body {
         width: 100%;
         height: 100%;
       }
       body {
         position: relative;
       }
       .outer {
         width: 100px;
         height: 100px;
         background: pink;
   
         position: absolute;
         top: calc(50% - 50px);
         left: calc(50% - 50px);
       }
     </style>
   </head>
   <body>
     <div class="outer">
       <!-- <div class="inner"></div> -->
     </div>
   </body>
   </html>
    ```
   
4. flex

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>Document</title>
     <style>
       * {
         margin: 0;
         padding: 0;
       }
       html, body {
         width: 100%;
         height: 100%;
       }
       body {
         display: flex;
         justify-content: center;
       }
       .outer {
         width: 100px;
         height: 100px;
         background: pink;
   
         align-self: center;
       }
     </style>
   </head>
   <body>
     <div class="outer">
       <!-- <div class="inner"></div> -->
     </div>
   </body>
   </html>
   ```

5. transform

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>Document</title>
     <style>
       * {
         margin: 0;
         padding: 0;
       }
       html, body {
         width: 100%;
         height: 100%;
       }
       body {
         position: relative;
       }
       .outer {
         width: 100px;
         height: 100px;
         background: pink;
   
         position: absolute;
         top: 50%;
         left: 50%;
         transform: translate(-50% , -50%);
         /* transform: translateY(-50%) translateX(-50%); */
       }
     </style>
   </head>
   <body>
     <div class="outer">
       <!-- <div class="inner"></div> -->
     </div>
   </body>
   </html>
   ```

   

### 居中元素宽高未知

1. 设置line-height与父元素高度一致，只适用于一行文本。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .box {
      margin: 100px auto;
      width: 200px;
      height: 200px;
      background: pink;
      text-align: center;
    }
    span {
      line-height: 200px;
    }
  </style>
</head>
<body>
  <div class="box">
    <span>你好啊</span>
  </div>
</body>
</html>
```

2. flex 通上

3. transform 通上

4. table-cell

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>Document</title>
     <style>
       * {
         margin: 0;
         padding: 0;
       }
       html, body {
         width: 100%;
         height: 100%;
       }
       div {
         width: 500px;
         height: 500px;
         background-color: aqua;
         display: table-cell;
         vertical-align: middle;
         text-align: center;
       }
     </style>
   </head>
   <body>
     <div>
       <span class="outer">垂直居中</span>
     </div>
   </body>
   </html>
   ```

   如果子元素是块级元素，那么就需要设置为， `inline-block`

5. 使用 table 布局



水平居中：

1. margin: 0 auto;
2. 文本： text-align: center
3. justify-content: center;