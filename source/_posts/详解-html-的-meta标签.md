---
title: 详解 html 的 meta标签
top: false
cover: false
toc: true
mathjax: true
date: 2020-11-10 11:44:44
password:
summary:
tags: 'html'
categories:
---

> 所有浏览器都支持 <meta> 标签

<meta> 元素可提供有关页面的元信息（meta-information）[元数据不会显示在客户端，但是会被浏览器解析]，比如针对搜索引擎和更新频度的描述和关键词。


<meta> 标签位于文档的头部，不包含任何内容。<meta> 标签的属性定义了与文档相关联的名称/值对。

meta必需的属性：

> content: 定义与 http-equiv 或 name 属性相关的元信息

可选属性

> | 属性               | 值                                                           | 描述                                |
> | ------------------ | ------------------------------------------------------------ | ----------------------------------- |
> | http-equiv         | content-type <br />expires<br />refresh<br />set-cookie      | 把 content 属性关联到 HTTP 头部     |
> | name               | author <br />description <br />keywords<br />generator <br />revised <br />others | 把 content 属性关联到一个名称。     |
> | scheme             | some_text                                                    | 定义用于翻译 content 属性值的格式。 |
> | charset [h5新属性] | UTF-8 or other                                               | 定义文档的字符编码。                |

实例

1. **定义文档关键词，用于搜索引擎**

   <meta name="keywords" content="HTML, CSS, XML, XHTML, JavaScript">

2. **定义web页面描述**

   <meta name="description" content="Free Web tutorials on HTML and CSS">

3. **定义页面作者**

   <meta name="author" content="Hege Refsnes">

4. **每30秒刷新页面**

   <meta http-equiv="refresh" content="30">