---
title: 如何置顶和加入文章封面
date: 2023-05-10 16:57:23
tags: hexo
categories: 博客搭建
description: 今天天气真好，下雨了，哈哈哈！
sticky: 1
---
![](images/ab.png)
可以直接在文章的front-matter区域里添加 sticky: 1 属性来把这篇文章置顶。数值越大，置顶的优先级越大。
同样，在Front-matter添加cover，并填上要显示的图片地址。
![](/images/zd.png)
如果不想在首页显示 cover, 可以设置为 false。
>文章封面的获取顺序 Front-matter 的 cover > 配置文件的 default_cover > false

```
cover:
  # 是否显示文章封面
  index_enable: true
  aside_enable: true
  archives_enable: true
  # 封面显示的位置
  # 三个值可配置 left , right , both
  position: both
  # 当没有设置cover时，默认的封面显示
  default_cover: 
```

## 如何网站加载速度优化
**压缩静态资源**
  静态资源，顾名思义，就是不会变化的资源。当然这个不会变化并不是指这个资源永远不会变，而是在网站更新前不会自己发生变动。最常见的静态资源包括但不限于：HTML文件、多媒体文件（图片、影音……）、字体文件、JS/CSS文件……

  我们先说HTML以及JS/CSS文件，这一类由代码构成的文件，在我们进行编写时，为了提高可读性，会插入很多的空格、换行等等字符。这些字符有些看得见有些看不见，其存在与否都不会影响运行结果，但其是确确实实占用着空间的，所以使用工具删掉这些字符就能减小一部分体积。

**方法：**
  接下来就是说明我是用的压缩方案，我是使用gulp来压缩静态资源。
  首先，我们要安装gulp，在博客根目录打开终端，输入：
```
npm install --global gulp-cli
npm install gulp -g   
npm install gulp --save  
```

  接下来，我们要安装gulp插件，小伙伴根据自己需要进行安装即可，不需要全部安装：
```
# 压缩HTML
npm install gulp-htmlclean --save-dev
npm install gulp-html-minifier-terser --save-dev

# 压缩CSS
npm install gulp-cssnano --save-dev

# 压缩JS
npm install gulp-terser --save-dev

# 压缩TTF
npm install gulp-fontmin --save-dev

# 压缩图片
npm install --save-dev gulp-imagemin
```
![](/images/abc.png)

**然后在根目录下创建【gulpfile.js】文件，并输入以下内容：**
```
const gulp = require("gulp")
// 用到的各个插件
const htmlMin = require('gulp-html-minifier-terser')
const htmlClean = require('gulp-htmlclean')
const terser = require('gulp-terser')
const cssnano = require('gulp-cssnano')
const fontmin = require('gulp-fontmin')

// 压缩js
// 参数 doc：https://github.com/terser-js/terser#minify-options
gulp.task('minify-js', () =>
    gulp.src(['./public/**/*.js'])
        .pipe(terser({
            compress: {
                /** @see https://blog.csdn.net/weixin_39842528/article/details/81390588 */
                sequences: 50,
                unsafe: true,
                unsafe_math: true,
                pure_getters: true,
                ecma: true
            }
        }))
        .pipe(gulp.dest('./public'))
)

// 压缩css
// 参数 doc：https://cssnano.co/docs/what-are-optimisations/
gulp.task('minify-css', () =>
    gulp.src(['./public/**/*.css'])
        .pipe(cssnano({
            mergeIdents: false,
            reduceIdents: false,
            discardUnused: false
        })).pipe(gulp.dest('./public'))
)

// 压缩html
// 参数 doc：https://github.com/terser/html-minifier-terser#readme
gulp.task('minify-html', () =>
    gulp.src('./public/**/*.html')
        .pipe(htmlClean())
        .pipe(htmlMin({
            removeComments: true,                   // 清除html注释
            collapseWhitespace: true,               // 合并空格
            collapseBooleanAttributes: true,        // 压缩布尔类型的 attributes
            noNewlinesBeforeTagClose: false,        // 去掉换行符
            removeAttributeQuotes: true,            // 在可能时删除属性值的引号
            removeRedundantAttributes: true,        // 属性值与默认值一样时删除属性
            removeEmptyAttributes: true,            // 删除值为空的属性
            removeScriptTypeAttributes: true,       // 删除 `type="text/javascript"`
            removeStyleLinkTypeAttributes: true,    // 删除 `type="text/css"`
            minifyJS: true,                         //压缩页面 JS
            minifyCSS: true,                        //压缩页面 CSS
            minifyURLs: true                        //压缩页面URL
        }))
        .pipe(gulp.dest('./public'))
)

//压缩字体
function minifyFont(text, cb) {
    gulp
        .src('./public/fonts/*.ttf') //原字体所在目录
        .pipe(fontmin({
            text: text
        }))
        .pipe(gulp.dest('./public/fontsdest/')) //压缩后的输出目录
        .on('end', cb);
}

gulp.task('minify-ttf', (cb) => {
    var buffers = [];
    gulp
        .src(['./public/**/*.html']) //HTML文件所在目录请根据自身情况修改
        .on('data', function (file) {
            buffers.push(file.contents);
        })
        .on('end', function () {
            var text = Buffer.concat(buffers).toString('utf-8');
            minifyFont(text, cb);
        });
});

//压缩
gulp.task("zip", gulp.parallel('minify-js', 'minify-css', 'minify-html', 'minify-ttf'))
```
*最后配置下命令，在【package.json】找到“scripts",在其下server添加'&& hexo gulp'*
```
"scripts": {
    "build": "hexo generate",
    "clean": "hexo clean",
    "deploy": "hexo deploy",
    "server": "hexo gulp && hexo server"  # 这里把gulp 添加在前面
```
*每次运行hexo s就会自动执行。*

