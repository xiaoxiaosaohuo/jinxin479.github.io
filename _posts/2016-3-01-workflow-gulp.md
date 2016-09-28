---
layout: post
title: "理解gulp自动化"
date: "2016-3-01"
slug: "深入理解gulp自动化"
description: "作为一个前端狗，实在是忍受不了每次摁F5刷新页面，也忍受不了手动的去压缩代码。使用gulp构建自己的工作流再爽不过了."
category:
  - views
  - featured
# tags will also be used as html meta keywords.
tags:
  - 博客
  - Jekyll
show_meta: true
comments: true
mathjax: true
gistembed: true
published: true
noindex: false
nofollow: false
# hide QR code, permalink block while printing.
hide_printmsg: false
# show post summary or full post in RSS feed.
summaryfeed: false
## for twitter summary card with squared image and page description or page excerpt:
# imagesummary: foo.png
## for twitter card with large image:
# imagefeature: "http://img.youtube.com/vi/VEIrQUXm_hY/0.jpg"
## for twitter video card: (active for this page)
---

gulp是前端开发过程中对代码进行自动化构建的利器。它不仅能对资源进行优化，而且在开发过程中能够通过配置自动完成很多重复的任务，让我们可以专注于代码，提高工作效率。

<!--more-->

## gulp的API
使用gulp，我们需要知道4个基本的API：`gulp.task()`,`gulp.src()`,`gulp.dest()`,`gulp.watch()`；

### gulp.src()
输出（Emits）符合所提供的匹配模式（glob）或者匹配模式的数组（array of globs）的文件。 将返回一个 Vinyl files 的 stream 它可以被 piped 到别的插件中；
gulp常用的glob匹配规则和技巧：
{% highlight bash %}
* 能匹配 a.js, x.y, abc, abc/,但不能匹配a/b.js
*.* 能匹配 a.js, style.css, a.b,x.y
*/*/*.js 能匹配 a/b/c.js, x/y/z.js,不能匹配a/b.js, a/b/c/d.js
** 能匹配 abc, a/b.js, a/b/c.js, x/y/z, x/y/z/a.b,能用来匹配所有的目录和文件
**/*.js 能匹配 foo.js, a/foo.js, a/b/foo.js, a/b/c/foo.js
a/**/z 能匹配 a/z, a/b/z, a/b/c/z, a/d/g/h/j/k/z
a/**b/z 能匹配 a/b/z, a/sb/z,但不能匹配a/x/sb/z,因为只有单**单独出现才能匹配多级目录
?.js 能匹配 a.js, b.js, c.js
a?? 能匹配 a.b, abc,但不能匹配ab/,因为它不会匹配路径分隔符
[xyz].js 只能匹配 x.js, y.js, z.js,不会匹配 xy.js, xyz.js等,整个中括号只代表一个字符
[^xyz].js 能匹配 a.js, b.js, c.js等,不能匹配 x.js, y.js, z.js
当有多种匹配模式时可以使用数组：gulp.src(['js/*.js','css/*.css','*.html'])
{% endhighlight %}



### gulp.dest()
`gulp.dest(path[, options])`
能被 pipe 进来，并且将会写文件。并且重新输出（emits）所有数据，因此你可以将它 pipe 到多个文件夹。如果某文件夹不存在，将会自动创建它。文件被写入的路径是以所给的相对路径根据所给的目标目录计算而来。类似的，相对路径也可以根据所给的 base 来计算。




### gulp.task()
`gulp.task(name[, deps], fn)`
* name 任务的名字，如果你需要在命令行中运行你的某些任务，那么，请不要在名字中使用空格。
* deps 一个包含任务列表的数组，这些任务会在你当前任务运行之前完成。
* fn 该函数定义任务所要执行的一些操作。通常来说，它会是这种形式：gulp.src().pipe(someplugin())

### gulp.watch
监视文件，并且可以在文件发生改动时候做一些事情。它总会返回一个 EventEmitter 来发射（emit） change 事件。

### 常用插件
1. gulp-load-plugins  这个插件能自动帮你加载package.json文件里的gulp插件
2. gulp-rename 用来重命名文件流中的文件。用gulp.dest()方法写入文件时，文件名使用的是文件流中的文件名，如果要想改变文件名，那可以在之前用gulp-rename插件来改变文件流中的文件名。
3. gulp-uglify 用来压缩js文件，使用的是uglify引擎
4. gulp-browserify 比起RequireJS，SeaJS这些模块化加载器： 不需要在js外面额外包个define(function(require, exports, module) {})，不用遵循AMD或者是CMD规范，代码更符合Node.js 风格的 CommonJS 模块编写规范。browserify有基于npm的依赖自动管理功能，可以自动下载一个类库的依赖，并将所有依赖打包成一个js文件， 并且页面不需要引入browserify。
5. gulp-minify-css css文件压缩
6. gulp-minify-html html文件压缩
7. gulp-jshint js代码检查
8. gulp-concat 用来把多个文件合并为一个文件,我们可以用它来合并js或css文件等，这样就能减少页面的http请求数了
9. gulp-sass 用sass编写css
10. gulp-imagemin gulp-imagemin插件来压缩jpg、png、gif等图片。
11. browser-sync   这可是个神器，能让浏览器实时、快速响应您的文件更改（html、js、css、sass、less等）并自动刷新页面。更重要的是 Browsersync可以同时在PC、平板、手机等设备下进项调试。您可以想象一下：“假设您的桌子上有pc、ipad、iphone、android等设备，同时打开了您需要调试的页面，当您使用browsersync后，您的任何一次代码保存，以上的设备都会同时显示您的改动”。[browser-sync](http://www.browsersync.cn/)
12. gulp-clean 清理编译环境
以上的插件的使用方法在npm官网中都有，可以随时去看[npm](https://www.npmjs.com/)

### 我的gulpfile.js,在google的web-starter-kit的基础上结合自己的项目进行了修改
{% highlight js %}
'use strict';
import path from 'path';
import gulp from 'gulp';
import del from 'del';
import runSequence from 'run-sequence';
import browserSync from 'browser-sync';
import swPrecache from 'sw-precache';
import gulpLoadPlugins from 'gulp-load-plugins';
import {output as pagespeed} from 'psi';
import pkg from './package.json';
var fileinclude = require('gulp-file-include');
var filter = require('gulp-filter');
const $ = gulpLoadPlugins();
const reload = browserSync.reload;

gulp.task('lint', () =>
  gulp.src('app/scripts/**/*.js')
    .pipe($.eslint())
    .pipe($.eslint.format())
    .pipe($.if(!browserSync.active, $.eslint.failOnError()))
);

gulp.task('images', () =>
  gulp.src('app/images/**/*')
    .pipe($.cache($.imagemin({
      progressive: true,
      interlaced: true
    })))
    .pipe(gulp.dest('dist/images'))
    .pipe($.size({title: 'images'}))
);

gulp.task('copy', () =>
  gulp.src([
    '!app/*.html',
    'node_modules/apache-server-configs/dist/.htaccess'
  ], {
    dot: true
  }).pipe(gulp.dest('dist'))
    .pipe($.size({title: 'copy'}))
);
gulp.task('copyfonts', () =>
  gulp.src([
    'app/fonts/*'
  ], {
    dot: true
}).pipe(gulp.dest('dist/fonts'))
    .pipe($.size({title: 'copy'}))
);
gulp.task('copyiconfonts', () =>
  gulp.src([
    'app/iconfont/*'
  ], {
    dot: true
}).pipe(gulp.dest('dist/iconfont'))
    .pipe($.size({title: 'copy'}))
);

gulp.task('styles', () => {
  const AUTOPREFIXER_BROWSERS = [
    'ie >= 10',
    'ie_mob >= 10',
    'ff >= 30',
    'chrome >= 34',
    'safari >= 7',
    'opera >= 23',
    'ios >= 7',
    'android >= 4.4',
    'bb >= 10'
  ];

  return gulp.src([
    'app/styles/**/*.scss',
    'app/styles/**/*.css'
  ])
    .pipe($.newer('.tmp/styles'))
    .pipe($.sourcemaps.init())
    .pipe($.sass({
      precision: 10
    }).on('error', $.sass.logError))
    .pipe($.autoprefixer(AUTOPREFIXER_BROWSERS))
    .pipe(gulp.dest('.tmp/styles'))
    // Concatenate and minify styles
    .pipe($.if('*.css', $.cssnano()))
    .pipe($.size({title: 'styles'}))
    .pipe($.sourcemaps.write('./'))
    .pipe(gulp.dest('dist/styles'));
});

gulp.task('scripts', function() {
	return gulp.src('app/scripts/**/*.js')
            .pipe($.newer('.tmp/scripts'))
            .pipe($.sourcemaps.init())
            .pipe($.sourcemaps.write())
		    .pipe(gulp.dest('.tmp/scripts'))
		    .pipe($.uglify())
            .pipe($.sourcemaps.write('.'))
		    .pipe(gulp.dest('dist/scripts'))

});
gulp.task('html', () => {
  return gulp.src('app/**.html')
    .pipe(fileinclude({
          prefix: '@@',
          basepath: '@file'
        }))
    .pipe($.useref({
      searchPath: '{.tmp,app}',
      noAssets: true
    }))

    .pipe($.if('*.html', $.size({title: 'html', showFiles: true})))
    .pipe(gulp.dest('dist'));
});

gulp.task('clean', () => del(['.tmp', 'dist/*', '!dist/.git'], {dot: true}));

// gulp.task('build', ['styles', 'scripts', 'images','copy'], function () {
//   gulp.start('html');
// });
gulp.task('serve', ['html','scripts', 'styles','copy','copyiconfonts','copyfonts'], () => {
  browserSync({
    notify: false,
    logPrefix: 'WSK',
    scrollElementMapping: ['main', '.mdl-layout'],
    server: ['.tmp', 'dist'],
    port: 3005
  });

  gulp.watch(['app/**/*.html'], ['html',reload]);
  gulp.watch(['app/styles/**/*.{scss,css}'], ['styles', reload]);
  gulp.watch(['app/scripts/**/*.js'], ['scripts', reload]);
  gulp.watch(['app/images/**/*'], reload);
});

gulp.task('serve:dist', ['default'], () =>
  browserSync({
    notify: false,
    logPrefix: 'WSK',
    scrollElementMapping: ['main', '.mdl-layout'],
    server: 'dist',
    port: 3005
  })
);

gulp.task('default', ['clean'], cb =>
  runSequence(
    'styles',
    ['html', 'scripts', 'images', 'copy','copyiconfonts','copyfonts'],
    'generate-service-worker',
    cb
  )
);

gulp.task('pagespeed', cb =>

  pagespeed('example.com', {
    strategy: 'mobile'
  }, cb)
);

gulp.task('copy-sw-scripts', () => {
  return gulp.src(['node_modules/sw-toolbox/sw-toolbox.js', 'app/scripts/sw/runtime-caching.js'])
    .pipe(gulp.dest('dist/scripts/sw'));
});

  const rootDir = 'dist';
  const filepath = path.join(rootDir, 'service-worker.js');

  return swPrecache.write(filepath, {
    cacheId: pkg.name || 'web-starter-kit',
    importScripts: [
      'scripts/sw/sw-toolbox.js',
      'scripts/sw/runtime-caching.js'
    ],
    staticFileGlobs: [
      `${rootDir}/images/**/*`,
      `${rootDir}/scripts/**/*.js`,
      `${rootDir}/styles/**/*.css`,
      `${rootDir}/styles/**/*.scss`,
      `${rootDir}/*.{html,json}`
    ],
    stripPrefix: rootDir + '/'
  });
});
{% endhighlight %}