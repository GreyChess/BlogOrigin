---
title: Livere插件在某些主题下无法正常显示的问题
layout:     post
category:   公开博客
date:       2018-09-20
author:     "Qian Yichao"
tags:
    - Livere        
---

Livere是非常好用的一款第三方社交评论插件，在搭建简单的门户网站或者个人博客的时候可以考虑使用。
<!-- more -->

### 1. 添加Livere插件
&emsp;&emsp;首先是登录[Livere](https://livere.com)的官网进入安装页面，以City版为例，填写内容可以略过，直接查看Code Managing这一栏
![DefaultHexo](/images/blogImage0922/livereInstall.jpg)
&emsp;&emsp;可以写一个简单的demo测试一下，把以上代码拷进.txt文本文件，把后缀名改为.html就可以看到评论框了，这个时候就可以登录评论了。
![DefaultHexo](/images/blogImage0922/livereDemo.jpg)
  相似的，把安装代码粘贴到你的页面下方，你的网站就拥有Livere的评论功能了。

### 2. Livere事件冲突
&emsp;&emsp;Livere的安装过程很简单。但有一个问题，Livere考虑到了页面性能的问题，在页面没有下滚到“lv-container”可见的时候，Livere对话框元素是不会加载的。参考源码：
![DefaultHexo](/images/blogImage0922/LivereIsNotWork.jpg)
&emsp;&emsp;Livere监听了“scroll”事件，当页面下滚到“lv-container”可见的时候，事件被注销，同时Livere正式加载。那么问题就是当“scroll”事件被别的插件拦截的时候，Livere就会无法监听，在这种情况下，评论对话框就无法正常加载。
&emsp;&emsp;很不巧，博主就遇到了这么一个奇葩的问题，就如同上图中所示，虽然Livere代码加在页面最后，但下拉到底的时候评论对话框任然无法正常显示。初步判断可能是本博客所用主题中的perfect-scroll插件拦截了scroll事件。
&emsp;&emsp;接下来我来说一下我解决这个问题的方法。首先是将Livere的安装js文件embed.dis.js下载到项目目录下面，修改
``` bash
j.src='https://cdn-city.livere.com/js/embed.dist.js'
```
指向我项目下面的安装文件。然后修改这个文件，找到
``` bash
livere.loading=function(){...}
```
把函数里面的内容都删了，在里面重新添加
``` bash
location.search.indexOf("redirectOrigin=true")>-1?wiget.oauth.call(this):livere.start.call(this)
```
然后重新启动项目，就能正常加载评论对话框了。

### 3. 其他
&emsp;&emsp;其实个人感觉disqus功能要更强大一些，但出于加载速度原因，disqus在国内几乎用不了。还有一个有意思的评论系统是gitcomment，使用git里面的指定repository下的issues来记录、加载评论，感觉git要被玩坏了。Livere的City版本很轻，但评论统计和新评论的提示这些还是齐全的，对于个人用户来说已经足够了。

