---
title: "git远程仓库连接"
date: 2020-02-04T22:47:53+08:00
tags: ["git远程仓库"]
categories: ["Git"]
draft: false
---

## 1. git远程仓库有哪些？

##### 1）[GitHub](https://github.com/)：目前最流行的国外的代码托管仓库，大佬比较多，纯英文。

##### 2）[码云](https://gitee.com/)：开源中国提供的代码托管产品

##### 3）[GitLab](https://about.gitlab.com/)：国外的git仓库管理系统。

##### 3）[Coding](https://coding.net/)：腾讯战略投资的代码托管产品

## 2. 本地git仓库与远程仓库的连接方式

这里以远程连接github仓库为例，本地仓库与远程仓库是两个独立的仓库，我们要做的是将本地的仓库内容复制一份传到远程仓库中，并且方便以后再从远程仓库下载下来继续编辑。

本地git仓库与远程仓库的连接有两种方式，一种是https连接，一种是ssh连接，https每次连接都需要输入账号密码，并且还不安全，很少人用，大部分都用更方便和更安全的ssh连接。

ssh连接是根据公钥、私钥加密解密的方式进行连接，原理就是在本地仓库所在的设备上(你的电脑)上放置私钥，在远程仓库设备上(github)放置公钥，然后就可以轻松传东西了。

## 3. ssh连接步骤

GitHub上有具体帮助文档可供参考：[GitHub帮助文档](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

码云上也有具体帮助文档可供参考：[码云帮助文档](https://gitee.com/help/articles/4181#article-header0)

以下命令是运行在git bash命令终端的命令

#### 3.1 生成公钥、私钥密匙对

```bash
ssh-keygen -t rsa -b 4096 -C 你的邮箱地址 //github

//ssh-keygen -t rsa -C 你的邮箱地址  //码云

//然后会出现提问的问题，按三次回车就可以
```

生成的ssh文件在用户目录中`C:\Users\Administrator\.ssh`，如果有用户名的就是用户名，我的直接是Administrator，该.ssh文件夹下放置的就是生成的公钥私钥密匙对，文件如下：

1）id_rsa：私钥文件，不能给别人看，自己解密用的。

2）id_rsa.pub：公钥文件，放到远程仓库所在的地方。

3）known_hosts：记录和当前设备(电脑)远程连接的设备，如github、码云等(配对成功后才写入的)。

#### 3.2 获取公钥内容

可用命令行获取到公钥内容，并复制放置在远程仓库设备对应位置中。

```bash
cat ~/.ssh/id_rsa.pub
```

#### 3.3 将公钥放置远程仓库处

![git_pic01](/imgs/git_pic01.jpg)



![git_pic02](/imgs/git_pic02.jpg)

![git_pic03](/imgs/git_pic03.jpg)

![git_pic04](/imgs/git_pic04.jpg)

#### 3.4 查看是否连接成功

在终端输入以下命令，其中的-T是test的意思

```bash
ssh -T git@github.com //github

//ssh -T git@gitee.com // 码云
```

输入上述命令后，github会给你一个公钥证明是它，让你接收，输入yes接收就好，只在开始的时候会需要输入，以后访问就不需要了。

然后yes回车后显示hi，“你的用户名”,You've successfully authenticated。。。

好了，你连接成功了。可以将本地仓库推到远程仓库了，连接命令在github或者码云新建仓库（不要勾选添加README文件），里面有对应的连接命令，不用记。

