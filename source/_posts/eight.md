---
title: hugo主题meme
date: 2023-05-22 17:41:09
tags:
---
#### hugo与hexo之异同
Hexo 是一个博客框架，Hugo 是一个网站框架。
hugo和hexo中mk语法还是有些不同的，比方front matter用来配置文章的标题、时间、链接、分类等元信息，提供模板调用。hugo中的写法：
```hugo
title: "post title"
date: "2023-08-20'
tags: ["tag1","tag2","tag3"]
categories: ["cat1", "cat2"]
weight: 20
```
Hugo 是一个基于 Go 语言开发的静态网站生成器（SSG），目前由 @bep 领衔开发，Hugo 的突出特点是简洁、灵活、高效，目前有很多知名网站都在使用 Hugo：Netlify、Let’s Encrypt、IPFS、Cloudflare Developers、DigitalOcean Docs、1Password 等等。与目前国内流行的 Hexo 相比，Hugo 的速度可称为飞速——在安装和使用上都是如此。
>
>~/blog $ tree -L 1
>.                     # 说明             Hexo
>├── archetypes/     # 文章模板          scaffolds/
>├── assets/         # Hugo 管道
>├── config.toml     # 配置文件          _config.yml
>├── content/        # 文章目录          source/_posts/
>├── data/           # Hugo 数据文件     source/_data/
>├── layouts/        # 布局模板
>├── public/         # 生成的静态文件     public/
>├── resources/      # Hugo 缓存
>├── static/         # 网站的静态文件     source/
>└── themes/         # 主题目录          themes/
>

对于文章摘要的截取，即「阅读更多」上方的内容。在 Hexo 中你可以在文章中加入
`<!-- more -->`来控制，但这在 Hugo 中是不会生效的，在 Hugo 中你必须将空格删除，即 `<!--more-->`
还有一个是 【index.md】 的问题，在 Hugo 中你必须在它的前面添加一个下划线，即 【_index.md】。比如：你想自定义标签页面的标题为中文，那么你先在新建一个 【content/tags/_index.md】 文件，然后在文件中加入：
```
title = "标签"
```

**在 Hexo 中，你每对文章进行一次修改，你就必须要在浏览器中手动刷新一下页面，如此才能看到最新的渲染结果🐶。但在 Hugo 中，只要有相关变化，Hugo 就会自动为你刷新页面。也就是说，你可以即时预览😎！顺便安利一个有用的技巧，在配置文件上方添加 newContentEditor = "gedit"（修改 gedit 为你喜欢的编辑器名），就可以在每次 hugo new 新建文章后自动打开你喜欢的文本编辑器！**

---
#### 参考
1.[Hugo 主题 MemE 文档](https://io-oi.me/tech/documentation-of-hugo-theme-meme/)
2.[Hugo 与 Hexo 的异同](https://io-oi.me/tech/hugo-vs-hexo/#fnref:8)
3.[Hugo | 一起动手搭建个人博客吧](https://mantyke.icu/posts/2021/hugo-build-blog/)