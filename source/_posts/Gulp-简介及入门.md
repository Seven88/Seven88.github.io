---
title: Gulp 简介及入门
date: 2016-01-12 18:20:05
tags: [gulp, 前端构建]
---

### 什么是 Gulp？

Gulp 是一款强大的基于 Node.js 的前端构建工具。

### 什么是前端构建？

> 一句话：自动化。对于需要反复重复的任务，例如压缩（minification）、编译、单元测试、linting等，自动化工具可以减轻你的劳动，简化你的工作。(引用自：[Grunt 官网][1])

### 同类工具 Grunt 对比

 - 出道晚，人气更旺。
    目前 [Gulp 19k+ stars][2]，[Grunt 10k+ stars][3] on GitHub。
 - 比简单更简单。
    Gulp 遵循代码优于配置策略，Grunt 的配置通常让人眼花缭乱;
    Gulp 只有5个核心 API；
    Gulp 的插件更纯粹，单一的功能，坚持一个插件只做一件事。
 - 核心设计基于Unix流的概念，通过管道连接，不需要写中间文件。

### 安装 Gulp

**安装 Node.js**：
前往 [https://nodejs.org/][4]，Download，Install，Done！
npm (Node Package Manager) 会随着 Node.js 一起安装。

**全局安装 Gulp：**

```
npm install gulp -g
```

**项目根目录安装**

```
npm install gulp --save-dev --registry=https://registry.npm.taobao.org/
// 使用 --save-dev 会将 gulp 自动添加到 package.json 的 devDependencies
// 使用淘宝源
```
(*package.json 是什么？https://docs.npmjs.com/files/package.json*)

<!-- more -->

### 安装Gulp插件

**常用插件：**
sass的编译（[gulp-ruby-sass][5]）
压缩css（[gulp-minify-css][6]）
压缩js代码（[gulp-uglify][7]）
压缩图片（[gulp-imagemin][8]）
图片缓存，只有图片替换了才压缩（[gulp-cache][9]）
清除文件（[del][10]）
编译html模板（[gulp-usemin][11]）
顺序执行任务（[run-sequence][12]）
自动刷新页面（[gulp-livereload][13]）需浏览器插件配合使用: [Chrome插件下载][14]

```
// 单个安装
npm install gulp-uglify --save-dev
// 批量安装
npm install gulp-ruby-sass gulp-minify-css gulp-uglify gulp-imagemin gulp-livereload gulp-cache del gulp-usemin run-sequence --save-dev
```

### 加载插件

在根目录创建 `gulpfile.js` ：
```
var gulp = require('gulp'),
    uglify = require('gulp-uglify'),
    minifyCss = require('gulp-minify-css'),
    del = require('del'),
    usemin = require('gulp-usemin'),
    imagemin = require('gulp-imagemin'),
    cache = require('gulp-cache'),
    rev = require('gulp-rev'),
    runSequence = require('run-sequence'),
    livereload = require('gulp-livereload');
```

### 创建任务

**先看一下 [Gulp API][15]**

**继续 code:**
```
// 压缩图片任务
gulp.task('build-img', function() {
    return gulp.src('img/**/*.{gif,jpeg,jpg,png}')
        .pipe(cache(imagemin({progressive: true})))
        .pipe(gulp.dest('dist/img'));
});

// deploy css
gulp.task('deploy-css', function() {
    return gulp.src('dist/css/**/*.*')
        .pipe(gulp.dest('../myapps/static/css/'));
});

// 清除目录
gulp.task('clean', function(cb) {
    return del(['.tmp', 'dist'], cb);
});

// 设置默认任务
gulp.task('default', ['clean'], function() {
    // 依次执行任务
    runSequence('task0', // task0 为任务名，比如上面的 build-img、clean
                ['task1-a', 'task1-b', 'task1-c'],  // 并行执行的任务
                'task2',
                function () {
                    // do sth after tasks done
                });
});

// watch 任务
gulp.task('watch', function() {
    // 监听
    livereload.listen();

    // 监听 img
    gulp.watch('img/**/*.{gif,jpeg,jpg,png}', ['build-img']);

    // dist 目标有变动则执行系列任务后，自动刷新页面
    gulp.watch('dist/**/*.*', function() {
        runSequence('deploy-css',
                    'deploy-img',
                    ...,
                    livereload.reload);
    });
});

```

### 执行任务

```
gulp
// 等同于
gulp default

// 执行监听任务
gulp watch
```

### 结束

更多详细内容请点击以上 gulp 及其插件链接。

  [1]: http://www.gruntjs.net/
  [2]: https://github.com/gulpjs/gulp
  [3]: https://github.com/gruntjs/grunt
  [4]: https://nodejs.org/en/
  [5]: https://github.com/sindresorhus/gulp-ruby-sass
  [6]: https://github.com/jonathanepollack/gulp-minify-css
  [7]: https://github.com/terinjokes/gulp-uglify
  [8]: https://github.com/sindresorhus/gulp-imagemin
  [9]: https://github.com/jgable/gulp-cache
  [10]: https://www.npmjs.org/package/del
  [11]: https://github.com/zont/gulp-usemin
  [12]: https://github.com/OverZealous/run-sequence
  [13]: https://github.com/vohof/gulp-livereload
  [14]: https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei
  [15]: https://github.com/gulpjs/gulp/blob/master/docs/API.md
