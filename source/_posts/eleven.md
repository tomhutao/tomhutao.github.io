---
title: hexo常见buff
date: 2023-05-25 09:47:09
tags: hexo 
---
**问题描述：**
在`hexo d`时报错，出现如下

```bash
*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'Administrator@TAOTAO.(none)')
FATAL {
  err: Error: Spawn failed
      at ChildProcess.<anonymous> (D:\hexo\read\node_modules\hexo-util\lib\spawn.js:51:21)
      at ChildProcess.emit (events.js:314:20)
      at ChildProcess.cp.emit (D:\hexo\read\node_modules\cross-spawn\lib\enoent.js:34:29)
      at Process.ChildProcess._handle.onexit (internal/child_process.js:276:12) {
    code: 128
  }
} Something's wrong. Maybe you can find the solution here: %s https://hexo.io/docs/troubleshooting.html

```

解决方法：
参考网上的解决方法就是找到.deploy_git中的隐藏文件.git(显示隐藏文件的方法自行百度)，再找到.git目录中的config文件，在最后边加上三行(其实其他地方也存在.git文件，如果不确定就把全部.git后面都加上下面三行)：
```
[user]
email=your email 
name=your name
```

