---
title: 初始化React项目
top: false
cover: false
toc: true
mathjax: true
date: 2020-10-27 09:42:13
password:
summary:
tags: 'react'
categories: '前端'

---

> 记一个完整的 `react` + `antd-mobile` + `redux`

0. 下载脚手架工具 `npm install -g create-react-app`
1. 初始化 react 项目: 
`create-react-app project-name`
2. 测试运行:
- 载入刚刚下载的目录：`cd project-name`
- 运行： `npm start`
- 查看结果： `localhost:3000`
3. 编码测试与打包发布项目
- 编码测试：
> - `npm start`
> - 访问网址： http://localhost:3000
> - 自动编译打包刷新(live-reload)
- 打包发布
> - `npm run build`
> - 全局安装`npm install -g serve`
> - `serve build`
> - 访问网址： http://localhost:5000
> - 如果不想使用 `serve build` 启动打包好的项目，也可以自定义 `package.json`文件的`scripts`, 如：

```
"scripts": {
    "prod": "serve build"
 }
```
这样子就可以通过 `npm prod`启动打包好的项目

4. 项目目录设计

```
- node_modules
- public
|-- favicon.icon
|-- index.html
- src
|-- api
|-- assets
|-- components
|-- containers
|-- redux
    |-- actions.js
    |-- actions-type.js
    |-- reducers.js
    |-- store.js
|-- utils
- index.js
- .gitignore
- package.json
- package-lock.json
- README.md
- yarn.lock
```

5. 引入`antd-mobile`
- 下载： `npm install antd-mobile --save`
- 页面处理: `index.html`
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <title>React App</title>
    <script src="https://as.alipayobjects.com/g/component/fastclick/1.0.6/fastclick.js"></script>
    <script>
      if ('addEventListener' in document) {
        document.addEventListener('DOMContentLoaded', function() {
          FastClick.attach(document.body);
        }, false);
      }
      if(!window.Promise) {
        document.writeln('<script src="https://as.alipayobjects.com/g/component/es6-promise/3.2.2/es6-promise.min.js"'+'>'+'<'+'/'+'script>');
      }
    </script>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```
- 组件打包方式与组件样式定制参考：https://www.cnblogs.com/serahuli/p/13569980.html

6. 引入路由 `react-router-dom`
`npm install --save react-router-dom`

7. 引入`redux`

`npm install --save redux@3.7.2 react-redux redux-thunk`

`npm install --save-dev redux-devtools-extension`

---
整合之后代码如下
创建路由组件：
#### containers/Register.jsx

```
import React, {Component} from 'react'

export default class Register extends Component {
  render() {
    return (
      <div>
        Register
      </div>
    )
  }
}
```
#### containers/Login.jsx

```
import React, {Component} from 'react'

export default class Login extends Component {
  render() {
    return (
      <div>
        Login
      </div>
    )
  }
}
```
#### containers/main.js

```
import React, {Component} from 'react'

export default class Main extends Component {
  render() {
    return (
      <div>
        Main
      </div>
    )
  }
}
```

#### redux/reducers.js

```
/*
 包含多个 reducer 函数， 根据旧的 state 和指定的 action 返回一个 新的 state
 */

import { combineReducers } from 'redux'

function XXX(state = 0, action) {
  return state
}

function YYY(state = 0, action) {
  return state
}

export default combineReducers({
  XXX,
  YYY
})
```
#### redux/store.js

```
/*
  redux 最核心的管理对象模块
 */

import { createStore, applyMiddleware } from 'redux'
import thunk from 'redux-thunk'
import { composeWithDevTools } from 'redux-devtools-extension'

import reducers from './reducers'

// 向外暴露 store
export default createStore(reducers, composeWithDevTools(applyMiddleware(thunk)))

```

#### index.js

```
import React from 'react'
import ReactDOM from  'react-dom'

// 路由
import { HashRouter, Route, Switch } from 'react-router-dom'
import Register from './containers/register/register'
import Login from './containers/login/login';

// store
import { Provider } from 'react-redux'
import store from './redux/store';


ReactDOM.render((
  <Provider store={ store }>
    <HashRouter>
      <Switch>
        <Route path='/register' component={ Register }></Route>
        <Route path='/login' component={ Login }></Route>
        <Route component={ Main }></Route>
      </Switch>
    </HashRouter>
  </Provider>
), document.getElementById('root'))

```

#### index.html

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <title>React App</title>
    <script src="https://as.alipayobjects.com/g/component/fastclick/1.0.6/fastclick.js"></script>
    <script>
      if ('addEventListener' in document) {
        document.addEventListener('DOMContentLoaded', function() {
          FastClick.attach(document.body);
        }, false);
      }
      if(!window.Promise) {
        document.writeln('<script src="https://as.alipayobjects.com/g/component/es6-promise/3.2.2/es6-promise.min.js"'+'>'+'<'+'/'+'script>');
      }
    </script>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>

```