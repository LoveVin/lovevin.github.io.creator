---
title: "如何使用GitHub Pages预览 HTML"
date: 2020-01-08T12:15:31+08:00
author: "LoveVin"
tags: ["GitHub", "HTML"]
categories: ["博客搭建"]
draft: false
---

### 1.GitHub提供免费域名
GitHub可以预览HTML文件，同时只要有一个GitHub账号，用户就有一个特定的免费域名，即用户名.github.io，比如我的GitHub账号名字为LoveVin，则全部换成小写后，我的免费域名为lovevin.github.io。

### 2.最短域名网站
用户可在GitHub创建一个与免费域名同名的仓库，如我的同名仓库为lovevin.github.io，然后将网站文件夹push进该仓库，然后在该仓库的settings里往下翻找到GitHub Pages 一项可以看到一个网址，该仓库对应的为用户网页，默认只能是master分支，点击该网址即可看到自己的网站，即通过免费域名访问的最短网址。

![这图片](/imgs/hugo14.JPG)

![这图片](/imgs/hugo15.JPG)

### 3.发布项目网站
GitHub预览HTML不仅仅局限于免费域名同名仓库，用户可建立其他HTML项目仓库，通过GitHub Pages访问，也是进入settings里，找到GitHub Pages，不过这里用户要自己选择分支。我这里选择的是master分支，好像可以选择其他分支，具体其他情况未尝试过。然后会得到一个网址，点击该网址即可访问，若不能访问就在该网址后加?...或者加具体网页名，如index.html。而且具体观察会发现，该项目仓库的网址也是免费域名/仓库名，像是域名下的一个文件夹，所以还是用户还是只有一个特定的GitHub免费域名。

![这图片](/imgs/hugo16.JPG)

![这图片](/imgs/hugo17.JPG)

### 4.绑定自定义域名
如果觉得GitHub的免费域名不够炫酷，可以自定义域名绑定在GitHub的域名上，自己买一个域名，添加至GitHub Pages里的Custom domain选项里保存即可。如上述2，图中红线圈出的位置。