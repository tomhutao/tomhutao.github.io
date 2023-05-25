---
title: 如何用hugo+github搭建博客
date: 2023-05-21 21:21:57
tags: 博客
categories: 博客搭建
sticky: 4
cover: https://img1.baidu.com/it/u=1881775613,643352686&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=333
---
本文逻辑：
**一、软件下载**
**二、配置环境变量**
**三、创建博客文件**
    1、创建站点文件夹
    2、下载主题
    3、新建博客
**四、将博客部署到github上**
***

## 一、软件下载
hugo和hexo类似，都是博客生成框架，hugo的优势是博客生成较快，而且安装比较简单，软件下载即安装成功。
本人电脑win7，所以首先下载对应版本的hugo。
hugo下载[HUGO](https://gohugo.io/)

## 二、配置环境变量
hugo安装完毕后在【hugo.exe】文件夹中，新建bin文件夹，将【hugo.exe】放入bin文件夹中。
然后设置环境变量：
>**控制面板->系统及安全性->系统->系统设定->环境变量path e:\hugo\bin(如果不添加path每次运行的时候要指定hugo的行对路径类似..\bin\hugo**，*这里个人把hugo下载在e盘中*)。

设置完成后，【win+r】输入cmd打开命令行，在命令行输入hugo version；git version分别查看环境变量是否添加成功，若打印版本号即配置成功，提示error则失败

## 三、创建博客文件
#### 1、创建站点文件夹
跳转到下载hugo的文件夹下，在windows命令行中用磁盘名冒号跳转到对应磁盘，进入文件夹用cd命令
比方，我的hugo文件夹在f盘就输入命令 f： 再输入cd 文件夹名称进入目录。
然后输入以下代码，生成站点文件夹
```
hugo new site myblog  #site后就是博客站点的名字，可以自己取
```
这样目录中就生成初始站点，站点目录
> archetypes/
> content/
> layouts/
> static/
> config.toml

#### 2、下载主题
由于hugo对新手不是很友好，所以安装包中没有任何主题，必须自己先下载好主题，主题可以在官网下载。[themes](https://themes.gohugo.io/).
选择喜欢的主题下载,点击Download跳转到该主题的github页面,点击clone or download.
比方,在命令行中克隆
```
git clone https://github.com/darshanbaral/meme.git
```

**主题下载完成后可以打开themes文件夹->进入主题文件->打开exampleSite文件夹->复制
exampleSite文件夹下的所有文件->返回myblog文件夹粘贴并替换相应文件**(通常跟着主题的文档有相应说明，跟着文章走就行)————【config.toml】是网页的配置文件，可根据需要进行配置，相关操作可参考主题下载页面下的文档

然后，返回上一级目录，本地启动博客，在命令行中输入：
```
hugo server
```
之后会有一个'http://localhost:1313/',本地博客网页就做好了。

#### 3、新建博客
打开git bash或cmd，输入
```
hugo new post\firstblog.md
```
返回终端，在新建博客站点的位置中【content/post/firstblog.md】可看到我们刚创建的博客，我们可以用vscode打开【firstblog.md】并写下自己的第一篇博客。之后输入:
```
hugo serever
```
即可本地网页预览自己刚写下的博客

## 四、将博客部署到github上
在你的github页面点击'new'新建一个存储仓库,仓库名称必须是小写且和github用户名相同.

命名格式为your_name.github.io ，随后点击create repository即可创建空仓库.

然后在本地hugo文件夹中输入：
```
hugo
```
hugo站点文件夹目录会多出一个public文件夹，这也是我们需要上传到github中的文件，我们在public文件夹中打开git bash，或者cd切换至public文件夹中，输入：
```
git init   #初始化
git add .
git commit -m "first commit"
git remote add origin https://github.com/your_name/your_name.github.io.git # 仓库地址
git push -u origin master #初次需要完整输入，后面只需git push
```
就此，个人博客就部署成功，可以在浏览器中输入your_name.github.io访问博客，一般github生成较慢，大概等个3-5分钟刷新网页即可。

以后再次写日志，push就只用输入：
```
cd public
git add .
git commit -m "xx"
git push
```

## 参考
1.[一起动手搭建个人博客吧](https://mantyke.icu/posts/2021/hugo-build-blog/)
2.[利用hugo与github仓库搭建免费博客](https://www.cnblogs.com/left23333/archive/2022/06/08/16349938.html)