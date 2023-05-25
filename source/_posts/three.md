---
title: 主题中播放器的设置（添加及隐藏）
date: 2023-05-13 02:13:34
tags: hexo
categories: 博客搭建
---

## 如何添加音乐播放器
### 安装插件
```bash
npm install hexo-tag-aplayer --save
```

### 配置

**第一步：**在站点配置文件【_config.yml】中新增配置项，由於需要全局都插入 aplayer 和 meting 資源，為了防止插入重複的資源，需要把 asset_inject 設為 false
在 Hexo 的配置文件中,建议直接加在最底下：
```yml
aplayer:
  meting: true
  asset_inject: false
```

**第二步：**在主題的配置文件中找到aplayerInject，enable 設為 true 和 per_page 設為 true
```yml
aplayerInject:
  enable: true
  per_page: true
```

**第三步：**把 aplayer代碼 插入到主題配置文件的 inject.bottom 去
aplayer html 例式：

```html
<div class="aplayer no-destroy" data-id="6990698783" data-server="netease" data-type="playlist" data-fixed="true" data-mini="true" data-listFolded="false" data-order="random" data-preload="none" data-autoplay="false" muted></div>
```

![p96FtoD.md.png](https://s1.ax1x.com/2023/05/13/p96FtoD.md.png)

在主题配置文件中找到inject，然后在bottom插入

```YAML
inject:
  head:
  bottom:
    - <div class="aplayer no-destroy" data-id="6990698783" data-server="netease" data-type="playlist" data-fixed="true" data-mini="true" data-listFolded="false" data-order="random" data-preload="none" data-autoplay="false" muted></div>
```

运行 Hexo 就可以看到网页左下角出现了 Aplayer.
最后，如果你想切换页面时，音乐不会中断。请把主题配置文件的 pjax 设为 true.

***


## 如何隐藏播放器——靠边隐藏

**第一步：**添加一下 CSS 样式使其自动缩进隐藏。在 【\themes\butterfly\source\css\custom.css】中 添加如下内容(如没有这个文件就新建一个[custom.css]) ：

```css
.aplayer.aplayer-fixed.aplayer-narrow .aplayer-body {
  left: -66px !important;
  /* 默认情况下缩进左侧66px，只留一点箭头部分 */
}

.aplayer.aplayer-fixed.aplayer-narrow .aplayer-body:hover {
  left: 0 !important;
  /* 鼠标悬停是左侧缩进归零，完全显示按钮 */
}
```

**第二步：**到主题配置文件引入自定义样式，修改【_config.butterfly.yml】的 inject 配置项：

```yml
inject:
  head:
    - <link rel="stylesheet" href="/css/custom.css"  media="defer" onload="this.media='all'">
```

最后重新运行hexo,看看左下角播放器是否隐藏了


   
