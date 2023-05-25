---
title: 一台设备如何部署多个github账户
date: 2023-05-21 00:38:53
tags: 博客，git
categories: 博客搭建
---
如果一台电脑上要使用两个github账号，前提条件是：
>1.能够生成两对私钥/公钥；
>2.push时能区分两个账户，推送到相应的仓库；

### 步骤一：生成两对钥匙
使用cd ~/.ssh切换工作目录，然后使用如下命令生成两个钥匙，中间一路回车
* 1、输入并回车：ssh-keygen -t rsa -C"你的第一个github邮箱地址"
* 2、输入并回车(这个是私钥的名称，可以随意取)：id_rsa_one
* 3、输入密码和再一次确认密码可以为空，回车
* 4、在.ssh目录下会出现私钥id_rsd_one和公钥id_rsa_one.pub
* 5、打开公钥id_rsa_one.pub，将内容copy到第一个github的SSH keys中

同理，配置第二个github邮箱地址：
```
ssh-keygen -t rsa -C"你的第二个github邮箱地址" -f id_rsa_second
```
生成名为id_rsa_second的密钥,然后将id_rsa_second.pub的内容copy到第二个github的SSH keys中。

>上面ssh-keygen 命令参数：
> -t: 指定生成rsa 类型秘钥
> -f: 指定生成秘钥的名字，可以不指定该参数，默认就会生成2个文件：私钥id_rsa，公钥 id_rsa.pub。因此上面的命令需要指定-f，否则生成两次后，私钥跟公钥会覆盖

### 步骤二：新建config文件
在.ssh目录下，新建一个config文件，配置内容如下: Host和User名称可以随意取，好辨识就行；HostName为github.com；IdentityFile配置为相应的私钥文件
```
# one                                                                       
Host onegithub
HostName github.com
User one
IdentityFile ~/.ssh/id_rsa_one

#second                                                                       
Host secondgithub
HostName github.com
User second
IdentityFile ~/.ssh/id_rsa_second
```

> 文件说明：
>Host：是HostName的别名，可以自己取，一般取跟HostName一样的名字。
>如果遮掩定义：Host mygithub，则在git clone时应如下输入：
>git clone git@mygithub:PopFisher/AndroidRotateAnim.git
>HostName：配置真正的域名
>PreferredAuthentications：配置登录时用什么权限认证，如：publickey,password >publickey,keyboard-interactive等
>User：用户名


### 步骤三： 绑定私钥
打开git bash输入如下命令：
```
ssh-agent bash
ssh-add id_rsa_one
ssh-add id_rsa_second
```
然后测试一下，是否绑定成功。输入如下命令：
```
ssh -T git@onegithub    #这里对应config中的别名Host
ssh -T git@secondgithub #这里对应config中Host
```
如果显示如下一段，表明绑定成功；
```
Hi one! You've successfully authenticated, but GitHub does not provide shell access.
```

### 步骤四：配置用户名和邮箱
**注意：因为一台电脑上配置了多个 github 账号，所以就不能再配置全局的用户名和邮箱了，而是在不同的仓库下，如果需要连接不同的 git 账号，配置相应的局部用户名和邮箱即可，如果之前配置过全局的用户名和邮箱，需要取消配置。**

首先清除全局配置：
```
# 取消全局 用户名/邮箱 配置
git config --global --unset user.name
git config --global --unset user.email
```

然后进入不同的仓库文件下，配置相应的name和email
```
git config user.email "你的第一个github邮箱地址"
git config user.name "one"

git config user.email "你的第二个github邮箱地址"
git config user.name "second"
```
如果需要重建origin,可执行下面操作：
```
git remote rm origin //清空原有的
git remote add origin git@one.github.com:one/test.git
```

本地新建仓库：
```
# 建立本地仓库
git init
git add -A
git commit -m "first commit"

# push 到 github上去
 git remote add origin git@one.github.com:one/test.git #关联远程仓库
 git push origin master
```
### 参考
1.[git多账户配置](https://steflerjiang.github.io/2016/12/16/git%E5%A4%9A%E8%B4%A6%E5%8F%B7%E9%85%8D%E7%BD%AE/)
2.[使用 SSH 连接到 GitHub（多帐号）](https://io-oi.me/tech/ssh-with-multiple-github-accounts/)