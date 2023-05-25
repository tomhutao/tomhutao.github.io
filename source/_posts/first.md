---
title: 第一次搭建博客
date: 2023-05-10 16:42:08
cover: https://img2.baidu.com/it/u=1273567368,2931564944&fm=253&fmt=auto&app=138&f=JPEG?w=320&h=480
tags: hexo
categories: 博客搭建
sticky : 5
---


  # hexo+Github搭建博客



作为一个小白，拒绝被裹挟，受够了各种自媒体平台的限制和恶心广告，于是萌生出搭建属于自己的博客的想法。虽然有些不自量力，但个人相信只要想做，没有什么是做不到的（很多事情不是‘做不做的到’的问题，而是’有没有决心‘的问题！）。

这个过程很痛苦，走了不少弯路，曾一度想放弃，可又不甘心，在抵触和坚持中终于搭建出自己的博客。

如果你也想搭建属于自己的博客，最重要是的什么？**勇气+坚持+耐心**，不要害怕遇到问题，问题是成长的基石，每一次的解决都是一次收获之旅。把问题当成一种挑战，一种向上发展的路劲，收获是不言而喻的。![](/images/ab.png)

## 前言

本人是使用**Hexo+Github**搭建博客，不熟悉这些工具的小白可能还是很懵的。简单说，就是使用**模板**（Hexo）搭建博客页面，生成本地博客，然后上传到**Github**服务器，由**github pages**渲染生成前端页面——网页。

####  

#### hexo的介绍

**Hexo**是一款快速、简洁且高效的博客生成框架。它基于Node.js,是搭建博客的首选框架。

它的优势是依赖少，易于安装和便于使用，可以直接使用Markdown语法撰写博客，然后将生成到网页上传到你的github上，之后别人就可以看到你的网页了。你无需关心网页代码的具体细节，只需专心写好博客的内容就行。

（因为**Hexo**的创建者是台湾人，对中文的支持很友好，可以选择中文进行查看。）

![](/images/abc.png)

#### github pages的介绍

使用**github pages**搭建博客的好处：

* 全是静态文件，访问速度快；

* 免费方便，不用花一分钱就可以搭建一个自由的个人博客，不需要服务器不需要后台；

* 可以随意绑定自己的域名，不仔细看的话根本看不出来你的网站是基于github的；

* 数据绝对安全，基于github的版本管理，想恢复到哪个历史版本都行

* 博客内容可以轻松打包、转移、发布到其它平台。



***

> 本文逻辑
>
> **第一部分：**环境准备；配置node.js和git环境，安装hexo，生成本地博客页面，下载和安装Vscode+Typora。
>
> **第二部分：**配置信息；注册github，创建仓库，绑定github，部署hexo到github，上传网页，完成搭建。
>
> **第三部分：**优化博客；下载主题，个性化装扮博客，备份博客源文件。

***



##  第一部分：环境准备

搭建博客其实很简单，只需利用**hexo**自动生成博客框架即可，但安装**hexo**前，电脑中必须要有Node.js和Git。因此，如果我们电脑中没有这些程序，首先就是安装Node.js和Git。

1.下载并安装Node.js；

2.下载并安装Git；

3.安装hexo，生成本地博客；



#### 1.下载并安装Node.js

**Node.js**的官网：https://nodejs.org/en

* 注意：Node.js版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本，否则后面运行**hexo**可能会遇到问题。

下载好对应你系统的Node.js版本后，剩下的就是傻瓜式的安装。这里有一点建议：如果你不是C盘战士，建议换个盘安装。

1.开始安装
![](images/nodejs1.png)

2.勾选复选框，点击【Next】按钮

![](/images/nodejs2.png)

3.修改目录，点击【Next】

![](images/nodejs3.png)

![](images/nodejs4.png)

![](/images/nodejs5.png)

4.后点击【Finish】完成安装

![](/images/nodejs6.png)



至此Node.js已经安装完成，可以先进行简单的测试看是否安装成功，后面还需要进行环境配置。



5.在键盘按下【win+R】键，输入cmd，然后回车，打开cmd窗口

![](images/nodejs7.png)



![](images/nodejs8.png)

安装完后的目录如下所示：

![](images/nodejs9.png)

**此处说明下**：新版的Node.js已自带npm，安装Node.js时会一起安装，npm的作用就是对Node.js依赖的包进行管理，也可以理解为用来安装/卸载Node.js需要装的东西



6.环境配置：

**注意**：这里的环境配置主要配置的是npm安装的全局模块所在的路径，以及缓存cache的路径，之所以要配置，是因为以后在执行类似：npm install express [-g] （后面的可选参数-g，g代表global全局安装的意思）的安装语句时，会将安装的模块安装到【C:\Users\用户名\AppData\Roaming\npm】路径中，占C盘空间。

例如：我希望将全模块所在路径和缓存路径放在我node.js安装的文件夹中，则在我安装的文件夹【D:\Develop\nodejs】下创建两个文件夹【node_global】及【node_cache】如下图：

![](images/nodejs10.png)

创建完两个文件夹之后，打开cmd命令窗口，依次输入：

```
npm config set prefix "D:\Develop\nodejs\node_global"
```

```
npm config set cache "D:\Develop\nodejs\node_cache"
```

![](/images/nodejs11.png)

接下来设置环境变量，关闭cmd窗口，“我的电脑”-右键-“属性”-“高级系统设置”-“高级”-“环境变量”

![](/images/nodejs12.png)


进入环境变量对话框，在【系统变量】下新建【NODE_PATH】，输入【D:\Develop\nodejs\node_global\node_modules】；

将【用户变量】下的【Path】修改为【D:\Develop\nodejs\node_global】。

![](images/nodejs13.png)

![](/images/nodejs14.png)

![](/images/nodejs15.png)

![](/images/nodejs16.png)
配置完成后，安装个module测试下——我们就最常用的express模块进行安装，打开cmd窗口，输入如下命令进行模块的全局安装：

```
npm install express -g  # -g是全局安装的意思
```

![](/images/nodejs17.png)

**至此Nodejs安装成功。**

***



#### 2.下载并安装git

* git的官网：https://git-scm.com/downloads

由于是国外网站，所以下载很慢，可以点一下链接。

* 链接：https://pan.quark.cn/s/d1f8086f2ac4 提取码：pGQm

下载完成后，同样是傻瓜式操作，建议不要安装在C盘。不清楚的可以看下面教程：

（安装教程：https://www.cnblogs.com/xueweisuoyong/p/11914045.html）

安装完成后，鼠标右键可以看到【Git Bash】和【Git GUI】就证明安装好了。

![](images/git_1.png)

***



#### 3.安装hexo，生成本地博客

**第一步：**在电脑的某个地方新建一个名为 blog 的文件夹（名字可以随便取）。

> 例如：我的是【D:\hexo\blog】，这个文件夹将来就作为你存放代码的地方。

**第二步：**在 【D:\hexo\blog 】文件夹下右键打开【 Git Bash Here】

![](/images/hexo2.png)

**然后窗口输入：**

```
npm install -g hexo-cli
```

**安装hexo，完成后再输入**：

```
hexo -v
```

**验证是否安装成功。**

![](/images/hexo.png)



**第三步：**初始化本地博客，在刚才的窗口中继续输入:

```
hexo init
```

```
npm install
```

这时我们的文件夹【D:\hexo\blog】中就多了些文件。

![](images/hexo5.png)

接着在命令窗口中输入：

```
hexo g
```

```
hexo s
```

![](/images/hexo6.png)

**本地博客页面**就此已生成，我们可以在浏览器中打开【http://localhost:4000/】，就可以看到我们的博客啦！

![](images/hexo4.png)

按【ctrl+c】可关闭本地服务器。



由于后面涉及到代码的修改及之后需要写博客，所以需要IDE工具。

常用的Markdown编辑器有：

* **Cmd Markdown**
* **Typora**（1.0版本后收费）
* **VScode**（需安装markdown all in one）

个人使用的是Vscode和Typora。当然你也可以只使用Vscode即可。

* Vscode官网：https://code.visualstudio.com/
* Vscode友情链接： https://pan.quark.cn/s/f64b7413660c 提取码：7eMQ
* Typora链接：https://pan.quark.cn/s/d36eb5eadc4c 提取码：Ze6B

***



## 第二部分：配置信息

本地生成的博客需要上传到服务器托管，然后才能通过网址进行访问。因此我们需要注册一个Github账户，在Github上创建仓库，将本地文件托管到这个远程仓库中，然后github会自动生成一个静态网页——github pages，我们可以通过这个网页访问到我们博客。

1.注册Github账户，创建仓库；

2.绑定Github；

3.部署博客到Github上。



#### 1.注册Github账户，创建仓库

**第一步：**注册Github账户

* Github官方网址：https://github.com/

![](/images/github1.png)

![](/images/github2.png)



**第二步：**创建个人仓库， 新用户注册完成后会自动跳转到创建页面。

![](/images/github3.png)

> **仓库的取名格式：用户名.github.io(这个就是你以后博客的网址)**

![](/images/github4.png)

点击create repository,完成仓库创建。



#### 2.绑定Github

**第一步：**回到你的git bash中，将本地与Github绑定一起，请输入：

```
git config --global user.name "liubei" //你的github用户名
```

```
git config --global user.email "xxx@xxx.com" //填写你的github注册邮箱
```

这里的name和email就是你注册Github的用户名和邮箱。



**第二步：**继续输入：

```
ssh
```

查看本机是否安装SSH。如果提示：No such file or directory，说明你是第一次使用git。

SSH（安全外壳协议，Secure Shell 的缩写）是建立在应用层基础上的安全协议。简单说，SSH就是保障你的账户安全，将你的数据加密压缩，不仅防止其他人截获你的数据，还能加快传输速度。

**为什么要配置这个呢？**

因为你提交代码肯定要拥有你的github权限才可以，但是直接使用用户名和密码不太安全，所以我们使用ssh key来解决本地与服务器的连接问题。



**第三步：**配置ssh，继续输入：

```
ssh-keygen -t rsa -C "你的github邮箱地址"
```

然后连续回车，一般3-4次。命令执行完成后，会在用户目录下生成一个文件（大致路劲：C盘—用户—Admin—.ssh文件夹），找到其中的【id_rsa.pub】，打开然后复制。

![](/images/github6.png)

> 简单讲，ssh就是一个秘钥，其中【id-rsa】是你这台电脑的私人秘钥，不能给别人看，【id-rsa.pub】是公共秘钥，可以给别人看。把这个公钥放在Github上，这样当你链接Github自己的账户时，它就会根据公钥匹配你的私钥，当相互匹配时，才能够顺利地通过git上传你的文件到Github上。

![](/images/github7.png)

接着在你的Github右上角找到setting，点进去找到SSH key的设置选项，点击New SSH key，把你刚才从【id_rsa.pub】中复制的信息粘贴进去，最后点击Add SSH key就可以了。

![](/images/github8.png)

![](/images/github9.png)

回到git bash验证是否成功，请输入：

```
ssh -T git@github.com
```

![](/images/github10.png)

第一次会出现这种情况，输入：yes，就行了。出现下图表示安装成功。

![](/images/github11.png)



#### 3.部署博客到Github上

**第一步：**这个时候我们需要先安装deploy-git，也就是部署命令。在git bash中输入：

```
npm install hexo-deployer-git --save
```

**第二步：**将hexo和Github关联起来，也就是将hexo生成的文章部署到Github上。在你的blog目录下找到【_config.yml】文件，打开并找到**deploy**进行修改。

![](/images/github12.png)

![](/images/github13.png)

```
deploy:
	type: git
	repo: git@github.com:username/username.github.io.git
	branch: main
```

repo中的内容即为github个人主页链接地址，不知道的可以打开仓库查看。

![](/images/github14.png)



**第三步：**部署文章，上线博客，输入：

```
hexo clean  #清除之前生成的东西
```

```
hexo g    #生成静态文章
```

```
hexo d   #部署博客
```

注意：第一次可能会弹出要你输入Github的username和password。完成后，你可以查看Github仓库，会发现多了很多文件，一般这就代表博客搭建成功，你可以用https://username.github.io登陆查看你的博客了。

![](/images/github15.png)

如果你的要求不高，其实就可以开始写博客了，直接在git bash 中输入：

```
hexo new "myimagesblog"
```

会在【source\ _post】文件夹中生成myimagesblog.md文件，你可以在这个文件中书写自己的博客，完成后上传文章就行。



***



![](/images/github16.png)

> **博客文件夹介绍**
>
> * _config.yml:俗称站点配置文件，很多与博客网站的格式、内容相关的设置都需要在里面修改。
> * node_modules:存储Hexo插件的文件，可以实现各种扩展功能。
> * package.json:我也不知道是干啥的。
> * scaffolds:模板文件夹，里面的post.md文件可以设置每一篇博客的模板。
> * source:非常重要，所有的个人文件都在里面。
> * themes：主题文件夹，可以从Hexo官网下载。



***



## 第三部分：优化博客

优化博客就是让自己博客更加美观，更加个性化，这里我们需要下载相应主题配置博客。

#### 1.下载主题

主题可以从hexo官网上下载，比较流行的主题是Next，Butterfly。个人配置的是Butterfly。

![](/images/tm1.png)

找到自己中意的主题，点进去，一般会跳转到github上，往下拉找到下载链接，复制下载，然后通过git下载。
![](/images/tm2.png)

直接输入：

```
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

```
npm install hexo-renderer-pug hexo-renderer-stylus --save
```

然后打开根目录下的【config.yml】文件，找到theme，修改为butterfly.

![](/images/tm3.png)

这样整个主题就配置成功，可以查看一下，输入：

```
hexo clean
hexo g
hexo d
```

***



#### 2.个性化设置

**修改语言：**在根目录下找到【_config.yml】文件，找到language。

![](/images/tm4.png)



**修改导航栏：**在主题配置文件中找到nav，把menu前面的‘#’去掉就行，将英文替换成中文。

![tm5](/images/tm5.png)

**修改头像：**在主题配置文件中找到avatar.

```
avatar:
	img: /img/avatar.png #将自己想要的图片保存在【theme/butterfly/source/img】中
	effect: true # 头像一直转
```

**修改顶部图：**找到index_img,同样是插入自己图片的路径

```
index_img: /img/XXX.png  #xxx是图片名称
```

**修改网站背景：**在主题配置文件中找到background，同样是插入图片地址，或者颜色。

```
background: url(/img/xx.png)  #img是保存图片的文件夹，xx是图片名 
```

**添加本地搜索：**先安装插件，输入：

```
hexo-generator-search
```

然后修改主题配置文件。

```
# Local search
local_search:
  enable: false # true 是开启本地搜索；false 是关闭
  # Preload the search data when the page loads.
  preload: false
  # Show top n results per article, show all results by setting to -1
  top_n_per_article: 1
  # Unescape html strings to the readable one.
  unescape: false
  CDN:
```

 **添加字数统计：**

打开hexo工作目录，输入：

```
npm install hexo-wordcount --save
```

然后修改主题配置文件

```
wordcount:
  enable: true  #改成true
  post_wordcount: true
  min2read: true
  total_wordcount: true
```



**侧边栏设置：**

在主题配置文件中找到aside，根据自己需要配置
