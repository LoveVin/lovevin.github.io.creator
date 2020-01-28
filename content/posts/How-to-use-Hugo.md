---
title: "如何用hugo搭建个人博客"
date: 2020-01-08T11:54:33+08:00
author: "LoveVin"
tags: ["hugo", "博客"]
categories: ["博客搭建"]
draft: false
---

### 1.hugo 的安装

#### 方法一

去 hugo 官网按照教程找对应版本的安装方法 [hugo 各系统安装](https://gohugo.io/getting-started/installing)

#### 其他 windows 安装方法

直接在 hugo 的 github 里下载资源包[hugo-github-release](https://github.com/gohugoio/hugo/releases)，在其中找到 windows 版本的 Assets，如下图：

![本图片](/imgs/hugo1.JPG)

下载后解压到自定义的软件文件夹内，然后解压后的如下图：

![本图片](/imgs/hugo2.JPG)

然后复制该.exe 文件所在的路径，添加至环境变量的 path 中，不知道环境变量配置的看文章最后图解。

配置成功后在命令窗口运行
`hugo version`
若能成功出现版本号，则表示安装成功，如下图所示：
![本图片](/imgs/hugo8.png)

### 2.hugo 创建博客

可按照 hugo 官方教程的创建步骤进行 [hugo 快速搭建博客](https://gohugo.io/getting-started/quick-start/)

具体创建代码和过程如下：

1. hugo new site 路径/创建的文件名 //在该指定路径下创建一个 hugo 工作文件夹，不加路径默认在命令行当前目录下创建，运行代码如下：

   ![本图片](/imgs/hugo9.png)

2. 创建完成后的文件夹里的文件如下：

   ![本图片](/imgs/hugo10.JPG)

   themes 文件夹里是放下载的博客主题，static 文件夹下放写博客需要的图片资源，content 文件夹下放写的博客内容

3. 进入创建的文件里，安装主题，可去网上找到想要的 hugo 主题，用 hugo clone 到 themes 中即可，不同主题的配置方式不同，具体按照找到主题的方式配置，本主题选择的教程为[Jane 主题教程](https://github.com/xianmin/hugo-theme-jane)。

4. 然后就根据选择的主题进行更改，每个主题要更改的方式不同，比较复杂。。。。我自己也没完全搞懂，待后续完善！

5. hugo 中创建一篇博客语句为`hugo new posts/my-first-post.md`，md 文件的编写语言是 markdown 语言的语法。

6. 在该文件夹下运行`hugo`命令会生成一个 public 文件夹，该文件夹就是将你写的 md 文件转化为可以在网页上运行的 html、css 文件等，是可以完整发布在 github 的。

7. 然后运行`hugo server`或者`hugo server -D`根据提示按住 ctrl 键点击生成的本地网址，预览生成的网页。注意要运行在 public 文件夹外的目录下

   `hugo server`：预览不包含草稿状态的页面

   `hugo server -D`：预览包含草稿状态的页面

8. 发布到 github 的时候只发布 public 文件夹即可，该文件夹另存储一下，该文件夹是博客页面生成源码，public 丢失时，再 hugo 一下本文件夹即可再生成 public 文件夹。

### 3.环境变量配置图解

![本图片](/imgs/hugo3.png)

![本图片](/imgs/hugo4.JPG)

![本图片](/imgs/hugo5.JPG)

![本图片](/imgs/hugo6.JPG)

![本图片](/imgs/hugo7.JPG)
