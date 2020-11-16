---
title: hexo + github 搭建个人博客入门
top: false
cover: false
toc: true
mathjax: true
date: 2019-6-27 09:34:31
password:
summary:
tags: 'hexo'
categories: 'hexo'
---

## 搭建一个属于自己的个人博客

1. [下载node]: http://nodejs.cn/download/

   验证下载成功：

   - 进入 命令控制符 Win + R
   - 输入`node -v`：出现版本号则为正确
   - 输入 `npm -v` ：出现版本号为正确

   ![image-20191123192721443](https://ftp.bmp.ovh/imgs/2019/11/d0ec9ce6b4304a0a.png)

2. [下载git]: https://git-scm.com/downloads

   下载成功：在空白处单击鼠标右键会出现：`git bash here` 和 `git GUI here`

3. 拥有自己的github账号

[注册链接]: https://github.com/

4. 生成SSH

   查看自己本机有没有SSH

   - 在终端输入 ： `ls -al ~/.ssh`

   ![image-20191123194054006](https://ftp.bmp.ovh/imgs/2019/11/f5e7175ef413e104.png)

   	存在`id_rsa` 和 `id_rsa.pub` 则本机有SSH

   - 或者在 c盘\用户\你的管理员 中有文件夹`.ssh`,文件夹下存在`id_rsa` 和 `id_rsa.pub` 两个文件，也可证明本机有SSH

   本机没有SSH，则需要生成

   - 在终端输入：` ssh-keygen -t rsa -C "your_email@example.com" `

5. 将 SSH 添加到 github 

   github中点击 `settings` -> ` SSH and GPG keys ` -> `New SSH Key` 

   验证：

   - 在终端输入

     `ssh -T git@github.com`

   - 如果成功则出现以下

     `Warning: Permanently added the RSA host key for IP address '52.74.223.119' to the list of known hosts.
     Hi serahuli! You've successfully authenticated, but GitHub does not provide shell access.`

     ![image-20191123195427521](https://ftp.bmp.ovh/imgs/2019/11/ec24940100c42740.png)

6. 在 github 上新建仓库（New Repository）

- 仓库名：`your github name.github.io`（这里的名字必须和你的 github 名字一致）

7. 在外网访问 的 网址

   ![image-20191123195555845](https://ftp.bmp.ovh/imgs/2019/11/7140cda32fd56299.png)

一直往下滑，会看到一个 `Github Pages`

![image-20191123195645759](https://ftp.bmp.ovh/imgs/2019/11/2f96e391bbafc7ad.png)

然后输入网址就可以看到属于自己的页面了。

8. 下载 `hexo`

   命令行输入：`npm install -g hexo`

9. 在电脑新建一个文件夹，用来存放你的博客

10. 进入你的博客文件夹：`git Bash Here` 

    执行以下命令：

    ```nginx
    hexo init #初始化
    hexo g #生成
    hexo s #开启本地预览服务
    ```

    本地预览开启之后就可以在浏览器输入 localhost:4000 访问，如果出现不可访问状态，则将localhost换成`127.0.0.1`这代表你的本机服务。

11. 对 hexo 进行配置

    打开博客目录的`_config.yml`文件，进行配置

    ```nginx
    # Site
    title: 你的博客名字
    subtitle: '副标题'
    description: '描述'
    keywords: "关键字"
    author: "作者"
    language: en
    timezone: ''
    
    deploy:
      type: git
      repository: git@github.com:serahuli/serahuli.github.io.git #你的github仓库链接，用SSH形式
      branch: master
    ```

12. 推送到公网：

    `hexo d` 成功后就可以在 你 Github Pages 上面的网址看到了

13. 推送新文章

    ```nginx
    hexo new "你的标题"
    hexo new page "你的标题"
    hexo generate
    hexo g
    hexo s
    ```

    [hexo 教程传送门：]: https://hexo.io/zh-cn/docs/

14. 改变主题：

    [主题传送门]: https://hexo.io/themes/

    通过git下载到 themes 文件夹下

    修改刚刚的 `_config.yml`下的 theme ，与你themes下的文件名一样即可

15. 写 博客是在 source 文件夹下

最后推荐一个写 markdown 的软件：Typore



============================================The ending