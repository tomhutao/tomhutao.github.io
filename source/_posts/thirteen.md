---
title: 如何给hugo博客文章加密（MemE主题）
date: 2023-06-11 00:14:59
tags: 博客
categories: 博客搭建
---

由于用的是MemE主题，所以给文章设置密码需要在主题文件中修改。

文件修改位置：\themes\meme\layouts\partials\header.html，用vscode打开文件，在末尾加入：

```
<script>
    (function(){
        if('{{ .Params.password }}'){
            if (prompt('请输入文章密码') !== '{{ .Params.password }}'){
                alert('密码错误！');
                history.back();
            }
        }
    })();
</script>
```
然后在想要加密的文章头部添加：password:xxxxx

```code
---
title: 随笔
password: xxxx   ## 这里xxx是你想设置的密码
---
```