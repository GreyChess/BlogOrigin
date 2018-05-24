---
title: 如何在github上优雅地建立自己的博客
layout:     post
date:       2018-05-24
author:     "Qian Yichao"
tags:
    - Hexo
excerpt: Hexo是一个前端的博客框架，需要注意的是这是一个比较专业化的框架，主要面对的是生成博客文章的静态页面。
---

在好友的撺掇之下，我也学着开始在网络上建立自己的博客。

### 1. 写在最开始的地方

本博客由[Hexo](https://hexo.io/)框架构建，发布于github。文笔水平有限，要是有没有讲到位的地方还请多多包涵。

### 2. 什么是Hexo

Hexo是一个前端的博客框架，需要注意的是这是一个比较专业化的框架，主要面对的是生成博客文章的静态页面。

### 3. 通过Hexo构建博客框架

> 本地需要安装: nodejs npm, git.

#### 在本地安装Hexo客户端

``` bash
$ npm install -g hexo-cli
```

#### 初始化Hexo工程

``` bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

其中，folder必须是一个空的文件夹。  
在初始化工程之后，工程目录看上去是这样的:

``` bash
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```
* _config.yml 是配置文件，博客信息和发布地址需要配置在这里，下面会有比较详细的配置方法。  
* package.json 做过nodejs开发的都知道，就不多说了。没做过的说了也无法理解，我也不多嘴了。 
* scaffolds 暂时用不上。  
* source 前端可以拿到的资源路径，博文（放在_posts文件夹下）以及图片音乐等相关资源可以存放在该目录下。  
* themes 当前博客的主题样式，好的样式可以把前端累死，当然我们更专注的博客内容，不必要花时间在优化主题上（有兴趣的可以自己写theme），同时Hexo提供了非常丰富的[主题](https://hexo.io/themes/)。

#### 启动本地预览
有意思的是hexo的server功能和它的核心功能是分开的，需要先安装hexo-server。
``` bash
$ npm install hexo-server --save   //If you do not have hexo-server installed.
$ hexo server
```
本地正常启动之后，在 localhost:4000 可以预览目前完成的博客内容。启动之后，搭载默认主题样式的博客大概是这个样子的：  
![DefaultHexo](/images/blogImage522/Hexo_default_theme.jpg)

### 4. 发布到个人github主页
>首先你要有一个github账户 ^_^，github相关的地方不再赘述

#### 添加hexo对支持git发布的包
``` bash
$ npm install hexo-deployer-git --save
```
#### 修改配置文件 _config.yml
``` bash
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
```
* repo: 个人的github首页ssh地址，标准格式: git&#64;github.com:&lt;yourUserName&gt;\&lt;yourUserName&gt;.github.io.git
* branch: 目标分支，这个一般用master就可以了。

#### 发布
``` bash
$ hexo deploy
```
现在你就可以登录自己的github主页了，地址是: &lt;yourUserName&gt;.github.io

### 5. 添加自己喜欢的主题
在[官方主题列表](https://hexo.io/themes/)里选择自己喜欢的主题样式，通过git clone到本地工程的themes文件夹下，修改 _config.yml
``` bash
theme: <target theme repo>
```
这样一来默认的主题就被替换成了你选择的主题样式。

#### hack主题样式
有这个需求的一般都是大牛级别的前端开发。话不多说，Hexo样式和页面结构采用ejs模板编写，有兴趣的[ejs官网](https://ejs.bootcss.com/)借一步说话。

### 6. 撰写博客
在source/_post下新建[markdown](http://www.markdown.cn/)文件，新加入的markdown文件在发布的时候自动加入到博客之中。更多与博客内容有关的还请自行体验。