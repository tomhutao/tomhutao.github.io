---
title: 如何备份博客源文件
date: 2023-05-12 11:26:42
tags: hexo
categories: 博客搭建
---


如果电脑中的本地博客文件丢失，或者不小心删除，又或者更换电脑，那我们该怎么办？
最好的办法就是备份一份源文件，当然你也可以每次写完博客后把它保存在U盘，虽然这个方法很保险，但不是很方便，毕竟不可能每次都把源文件拷进U盘。

最优化方案就是把博客源文件备份在远程仓库中，这样就算是更换电脑，或者本地文件丢失，我们也不用慌，可以从远程仓库把这个源文件下载下来，而且每次可以更新完博客之后，输入命令同步上传源文件。

因为hexo部署到github上的文件不包含源文件。详细的讲，在github仓库中的文件是由'hexo g'首先生成一个public文件————这个好像应该叫静态文件，再然后通过'hexo d'上传到github仓库中，这个时候本地也会有一个【.deploy_git】文件生成————这个就是上传的文件，这个里面的文件和【public】是一样的。
![](https://s1.ax1x.com/2023/05/12/p9ypHMT.png)
![](https://s1.ax1x.com/2023/05/12/p9ypbsU.png)

我们在进行备份时，并不需要将整个博客目录全部备份，只备份以下几个用户自定义的即可：scaffolds目录，source目录，themes目录，.gitignore文件，_config.yml文件，package.json文件，其他都是通用的。

>**首先我们先来观察整个博客目录的结构：**
>1) 【.deploy_git】 本目录会在我们部署时生成，也就是github上保存的文件，无需备份。
>2) 【node_modules】 本目录包含了hexo博客依赖的模块，安装时自动生成，无需备份。
>3) 【public】 与【.deploy_git】类似，是编译后生成的文件静态网页文件，无需备份。
>4) 【scaffolds】 保存了用户文章的模板，需要备份。
>5) 【source】 保存了用户文章的源文件，需要备份。
>6) 【themes】 保存了用户下载的主题文件与配置，需要备份。
>7) 【.gitignore】 保存了推送到github时忽略的文件名，需要备份。
>8) 【_config.yml】 保存了用户配置信息，需要备份。
>9) 【db.json】 保存了网页的数据文件，在编译生成静态网页时会自动更新，无需备份。
>10) 【package.json】 保存了依赖的模块列表，需要备份。
>11) 【package-lock.json】保存了依赖的模块安装记录，无需备份。

![p9yVJz9.png](https://s1.ax1x.com/2023/05/12/p9yVJz9.png)

**那么我们该如何备份呢？**
>**第一步：**登陆Github，在博客的仓库下新建一个分支，名字自己取(我的名叫Mblog)；
>**第二步：**然后在这个仓库中，按setting，将分支设置为defaul（默认）。

![p9yQ2an.png](https://s1.ax1x.com/2023/05/12/p9yQ2an.png)
![p9yQgVs.png](https://s1.ax1x.com/2023/05/12/p9yQgVs.png)

然后在本地的任意目录下，打开git bash，之后git clone仓库地址（个人是在hexo目录下打开），例如：个人执行的：
```
git clone git@github.com:xxxxxx/xxxxxxx.github.io.git # 后面地址是仓库的
# 一定要是ssh地址，不然后面的'git push'会报错，因为用https后面需要重现登陆github,但github从2021年8月30日之后又不支持用户名登陆，这就有点bug
```
![p9y8of1.png](https://s1.ax1x.com/2023/05/12/p9y8of1.png)
由于默认分支已经设成了Myblog，所以clone时只clone了Myblog。clone完成后本地会生成一个仓库名的文件。
>**第三步：**将克隆下来的目录中除了.git文件夹外的所有文件都删掉，如果看不到.git文件夹请打开显示隐藏文件夹
![p9y8OmD.md.png](https://s1.ax1x.com/2023/05/12/p9y8OmD.md.png)
>**第四步：**把之前我们写的博客源文件全部复制过来，除了.deploy_git。
这里应该说一句，复制过来的源文件应该有一个.gitignore，用来忽略一些不需要的文件，如果没有的话，自己新建一个，在里面写上如下，表示这些类型文件不需要git：

![p9ylQds.md.png](https://s1.ax1x.com/2023/05/12/p9ylQds.md.png)

* 注意：如果之前克隆过themes中的主体文件，要将主题文件中的.git目录删除掉，否则无法备份主题文件.因为git不能嵌套上传，最好是显示隐藏文件，检查一下有没有，否则上传的时候会出错，导致你的主题文件无法上传，这样你的配置在别的电脑上就用不了了。
![p9ylfwd.png](https://s1.ax1x.com/2023/05/12/p9ylfwd.png) 

>**第五步：**在该备份的目录下执行以下命令：
```
git add .
git commit -m "备份"
git push
```
这样你的博客就备份好了，可以在你的Github上看一看是否有这些源文件。其中node_modules、public、db.json已经被忽略掉了，没有关系，不需要上传的，因为在别的电脑上需要重新输入命令安装 。
![p9yBZrR.md.png](https://s1.ax1x.com/2023/05/12/p9yBZrR.md.png)

以后每次再更新文章，一定要把源文件上传一下，依次执行命令就行：
```
hexo clean
git add .
git commit -m "xxx"
git push
hexo g
hexo d
```

## 恢复博客
如果更换设备，那就在新设备上克隆就可以了
```
git clone 仓库地址
```
然后在克隆下来的文件夹中执行命令————即把hexo重新安装一遍
```
npm install hexo-cli
npm install 
npm install hexo-deployer-git
```
然后就可以正常使用了，同样要注意：**每次更新完文章，把源文件上传一下**
```
hexo clean 
git add .
git commit -m ""
git push
hexo g
hexo d
```
#### 参考
1.[Hexo博客备份](https://www.jianshu.com/p/57b5a384f234)
2.[hexo源码上传到GitHub](https://www.cnblogs.com/eidolonw/p/13066869.html)