---
title: 如何使用hexo搭建博客
date: 2018-07-27 23:04:43
categories: Hexo
tags: ["Hexo","Next"]
---

[Hexo](https://hexo.io/zh-cn/docs/index.html) 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

<!--more-->

# 安装前提
在安装 hexo 前，您必须检查电脑中是否已安装下列应用程序：

- [nodejs](https://nodejs.org/en/)
- [git](https://git-scm.com/)  

# 项目安装

本教程环境为win10，程序安装完成后，使用管理员权限打开控制台，使用npm完成对hexo的安装
```bash
$ npm install -g hexo-cli
```

安装完成后，新建空的项目文件夹，cd到该目录下后，对hexo初始化项目
```bash
$ hexo init
```

安装完成后，使用以下命令生成新的博客，生成的博客在`\source\_posts`目录下。
```bash
$ hexo new "mysirtblog"
```

然后清空缓，然后存生成静态文件
```bash
$ hexo clean

$ hexo generate
```
启动服务，预览效果
```bash
$ hexo server
```

运行后如下图所示  
{% asset_img hexo初始化运行效果.png %}

注：hexo默认使用4000端口，如果该端口已被其他程序占用（例如福昕pdf），会运行失败。可以指定端口运行: 
```bash
$ hexo server -p 5000
```

至此 hexo 全部安装完成。

# Next 博客模板

接下来我们安装 [Next](http://theme-next.iissnan.com/getting-started.html) 模板，该模板是一套非常简洁的博客模板，你也可以选择其他喜欢的模板安装。

## 安装Next模板
通过git下载模板，你也可以直接在git上下载该模板的zip包，然后解压到站点的themes目录下。

```bash
$ git clone https://github.com/theme-next/hexo-theme-next.git themes/next
```

下载完成后，cd到themes/next目录，初始化next的依赖包
```bash
$ npm install
```

## 启用主题
打开站点配置文件（根目录的_config.yml)，找到 theme 字段，并将其值更改为 next。
> theme: next

关于next更多的操作，可见官网。

## Hexo 常用命令
```bash
$ hexo new "mysirtblog"  *//新建博客*

$ hexo clean  //清空缓存数据

$ hexo generate  //生成博客静态文件

$ hexo server -p 5000  //运行博客站点，若不制定端口 -p 5000 ，则默认使用http://localhost:4000端口

$ hexo deploy  //发布站点
```