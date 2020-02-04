---
title: "命令行解释器"
date: 2020-02-04T22:45:34+08:00
tags: ["命令行解释器"]
categories: ["Git"]
draft: false
---

## 写在前面

命令行解释器是一个单独的软件程序，它可在用户和操作系统之间提供直接的通讯。命令行解释器是解释器的一种，用于对命令行进行解释执行。

#### shell

俗称"壳"，用来区别于操作系统内核，shell是一种命令语言，又是一种程序设计语言。用于负责用户和操作系统的交互。shell提供了用户与内核进行交互操作的一种接口，它接收用户输入的命令并把它送入内核去执行。shell在内核、系统调用之外，所以叫shell。

以下所列的命令行解释器是shell的一种。

## 1. Window操作系统

#### cmd (Command shell)：win7之前的旧版本

#### Powershell：win7之后提供的更高级的版本，cmd的升级版。

以上两个命令执行程序都在window中可找到。

## 2. Unix/Linux/MacOS等类Unix操作系统

#### Bash (Bash Shell)：最常用的一种shell

## 3. 关于Git的一些知识

我们初学git都知道是要安装git bash才能运行git命令，那么关于git bash你又知道多少？

#### Git

Git是一个用于版本控制的工具，最开始设计的时候是用在Unix风格的环境中，因此，一些基于Unix的类Unix操作系统如Linux、MacOS等都内置了Unix命令行终端Bash，因此git运行在类Unix的系统中不需要额外安装设什么东西，直接在其终端使用即可。

#### git Bash

由于Window操作系统是一个非Unix终端环境，其有自己的终端cmd和Powershell，因此无法运行git命令，因此才有了Git Bash工具，安装在Window环境上，提供模拟Unix环境，让在window上轻松运行git命令成为可能。因此git bash是git的模拟终端。

#### git Shell

Git shell是一个通过SSH访问的Git服务器的程序。

## 4. 在Windows上使用bash

#### 4.1 Cmder命令集合工具

#### 4.2 Cygwin环境(Unix模拟环境)

## 5. 在Windows上使用Git

#### 5.1 安装git bash工具

#### 5.2 安装Cmder命令集合工具(里面自带bash)





