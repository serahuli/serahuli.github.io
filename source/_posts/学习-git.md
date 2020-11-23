---
title: 学习 git
top: false
cover: false
toc: true
mathjax: true
date: 2020-11-17 16:32:48
password:
summary:
tags:
categories:
---

> 版本控制是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统。

Git 特点：

- 直接记录快照，而非差异比较

  > 每次你提交更新，或在 Git 中保存项目状态时，它主要对当时的全部文件制作一个快照并保存这个快照的索引。 为了高效，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。 Git 对待数据更像是一个 快照流。 

- 近乎所有操作都是本地执行 

- Git 保证完整性 

  > Git 中所有数据在存储前都计算校验和，然后以校验和来引用。
  >
  > 不可能在 Git 不知情时更改任何文件内容或目录内容。
  >
  > Git 用以计算校验和的机制叫做 SHA-1 散列（hash，哈希）。

- Git 一般只添加数据

Git 的三种状态：

- 已提交（committed）：表示数据已经安全的保存在本地数据库中
- 已修改（modified）：表示修改了文件，但还没保存到数据库中
- 已暂存（staged）：表示对一 个已修改文件的当前版本做了标记，使之包含在下次提交的快照中

![ Git 项目的三个工作区域的概念：Git 仓库、工作目录以及暂存区域](image-20201117164247683.png)

> - Git 仓库目录是 Git 用来保存项目的元数据和对象数据库的地方。 这是 Git 中最重要的部分，从其它计算机克隆仓库时，拷贝的就是这里的数据。 
> - 工作目录是对项目的某个版本独立提取出来的内容。 这些从 Git 仓库的压缩数据库中提取出来的文件，放在磁盘上供你使用或修改。 
> - 暂存区域是一个文件，保存了下次将提交的文件列表信息，一般在 Git 仓库目录中。 有时候也被称作“索引”，不过一般说法还是叫暂存区域。 

# 配置 Git 环境

Git 自带一个 git config 的工具来帮助设置控制 Git 外观和行为的配置变量。

**设置用户名称与邮件信息**

```bash
$ git config --global user.name "sera"
$ git config --global user.email sera@example.com
```

`--global` 是设置全局变量，如果不想设置全局，可以单独修改某个文件。

**检查配置项**

```bash
git config --list 	// 会找到每个变量的最后一次配置
git config <key>	// 单独检查某一项的配置：如 git config user.name
```

**请求帮助**

```bash
git help <verb>
git <verb> --help
man git-<verb>

git help config // get config file
```

# Git 基础

**在现有目录中初始化仓库 **

> ```bash
> // 创建一个名为 .git 的子目录, 含有初始化Git仓库中所有的必须文件
> $ git init  
> // 跟踪并且提交
> $ git add *.c 
> $ git add LICENSE 
> $ git commit -m 'initial project version'
> ```

**克隆现有仓库**

> ```bash
> // 克隆
> $ git clone [url]
> // 克隆并且重命名
> $ git clone [url] re-name
> ```

**检查文件状态**

```bash
$ git status
```

Changes to be committed

**跟踪新文件**

```bash
$ git add README
```

