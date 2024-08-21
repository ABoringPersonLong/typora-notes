# 1. 了解 Gulp

前端自动化打包构建工具

- 打包：把文件压缩、整合、移动、混淆

## 1. 了解一下前端的打包构建工具

- gulp：基于流的打包构建工具
- webpack：基于 js 文件的打包构建工具

## 2. 什么是流

- 流文件：流

  - 一种文件传输的格式
  - 一段一段的文件传输

- 流格式：流

  - 从头到尾的一个过程

  - 需要从源开始一步一步进过加工

    每一个步骤需要依赖上一步的结果

    最终给出一个完整的成品

- gulp 是基于流格式的一种打包构建工具

## 3. Gulp 的依赖环境

- 依赖于 node 环境进行开发
- 底层封装的内容就是 node 里面的读写文件

## 4. Gulp 的作用

- 对于 css 文件
  - 压缩
  - 转码（自动添加前缀）
- 对于 js 文件
  - 压缩
  - 转码（ES6 转 ES5）
- 对于 html 文件
  - 压缩
  - 转码（对格式的转换）
- 对于静态资源文件的处理
- 对于第三方文件的处理
- ...

## 5. Gulp 的安装

- gulp 是一个 js 相关的工具
- 可以直接使用 npm 进行安装
- 需要全局安装 gulp 命令行工具

```sh
npm i -g gulp-cli
```

## 6. Gulp 的版本

- gulp@3
  - 安装成功检测版本号 gulp 3.9.1
- gulp@4
  - 安装成功检测版本号 gulp cli 2.3.0

## 7. Gulp 检测版本

```sh
gulp --version
```

# 2. 使用 Gulp

## 1. 准备一个项目

- 你要确定好自己的目录结构
- 你要分开源码和打包以后的内容
- 必须要保证打包前后的目录结构一致
  - 创建一个叫做 src 的目录（表示源码）
  - 创建一个叫做 dist 的目录（存放打包后的文件）

## 2. 准备一个 gulpfile.js 的文件

- 必须有
- gulp 进行打包的依据
- 每一个项目需要一个 gulpfile.js
- 我们在这个文件里面进行本项目的打包配置
- gulp 在运行的时候，会自动读取 gulpfile.js 文件里面的配置
- 按照你在 gulpfile.js 文件里面的配置进行打包工作
- 注意：**直接写在项目根目录，和 src 同级**

## 3. 在项目里面再次安装 gulp

- 注意：**项目里面的 gulp 是以第三方模块的形式出现的**

- 专门给你提供配置打包流程的 API 的

- 每一个项目都要安装一次

  ```sh
  npm i -D gulp
  ```

- gulp 常用 API

  1. gulp.task()

     - 语法：gulp.task(任务名称, 任务处理函数)
     - 作用：创建一个基于流的任务
     - 例子：`gulp.task('htmlHandler', () => {})`

  2. gulp.src()

     - 语法：gulp.src(路径信息)

     - 作用：找到源文件

     - 例子：

       1. `gulp.src('./a/**')`

          相当于 `*.*`，找到指定目录下的所有文件

       2. `gulp.src('./a/**/*')`

          找到指定目录下的所有子目录的所有文件

  3. gulp.dest()

     - 语法：gulp.dest(路径信息)

     - 作用：把一个内容放入指定目录内

     - 例子：`gulp.dest('./abc')`

       把他接受到的内容放到 abc 目录下

  4. gulp.watch()

     - 语法：gulp.watch(路径信息, 任务名称)

     - 作用：监控指定目录下的文件，一旦发生变化，从新执行后面的任务

     - 例子：`gulp.watch('./src/views/*.html', htmlHandler)`

       当指定目录下的 html 文件发生变化，就会执行 htmlHandler 这个任务

  5. gulp.series()

     - 语法：gulp.series(任务1, 任务2, ...)
     - 作用：逐个执行多个任务，前一个任务结束，第二个任务开始

  6. gulp.parallel()

     - 语法：gulp.parallel(任务1, 任务2, ...)
     - 作用：并行开始多个任务

  7. pipe()

     - 管道函数
     - 所有的 gulp API 都是基于流
     - 接受当前流，进入下一个流过程的管道函数
     - 例子：`gulp.src().pipe(压缩任务).pipe(转码).pipe(gulp.dest('./abc'))`

## 4. 在 gulpfile.js 文件里书写配置

- 书写该项目的打包流程
- 书写完毕以后，按照打包流程去执行 gulp 指令运行 gulpfile.js 文件

## 5. gulp 常用插件

gulp 的各种插件就是用来执行各种各样的压缩混淆转码任务的。

1. gulp-cssmin

   - 压缩 css 文件

   - ```sh
     npm i -D gulp-cssmin
     ```

   - ```js
     const gulpCssmin = require('gulp-cssmin')
     gulpCssmin()
     ```

2. gulp-autoprefixer

   - 自动添加前缀（浏览器兼容性）
     
   - ```sh
     npm i -D gulp-autoprefixer
     ```

   - ```js
     const gulpAutoprefixer = require('gulp-autoprefixer')
     gulpAutoprefixer({ browsers: ['要兼容的浏览器'] }) // 兼容最近两个版本的浏览器
     gulpAutoprefixer() // 也可以将 browsers 的配置改写到 package.json 的 browserslist 里
     
     // package.json
     "browserslist": [
       "last 2 versions", // 兼容最近两个版本的浏览器
       "FireFox < 20", // 兼容 20 版本前的火狐
       "iOS < 7" // 兼容 7 版本前的苹果
     ]
     ```

3. gulp-sass

   - 将 sass 转换成 css
     
   - ```sh
     npm i -D gulp-sass sass
     ```
     
   - ```js
     const gulpSass = require('gulp-sass')(require('sass'))
     gulpSass()
     ```

4. gulp-uglify

   - 压缩 js 文件

   - ```sh
     npm i -D gulp-uglify
     ```

   - ```js
     const gulpUglify = require('gulp-uglify')
     gulpUglify()
     ```

5. gulp-babel

   - ES6 转 ES5

   - ```sh
     # 如果是 gulp@3，就安装 gulp-babel@7
     # 如果是 gulp@4，就安装 gulp-babel@8
     npm i -D gulp-babel @babel/core @babel/preset-env
     ```

   - ```js
     const gulpBabel = require('gulp-babel')
     gulpBabel({
       presets: ['@babel/env'] // 如果是 babel@7，就写 ['es2015']
     })
     ```

6. gulp-htmlmin

   - 压缩 html 文件

   - ```sh
     npm i -D gulp-htmlmin
     ```

   - ```js
     const gulpHtmlmin = require('gulp-htmlmin')
     gulpHtmlmin({ // 通过你配置的参数来进行压缩
       collapseWhitespace: true, // 移除空白（空格、换行）
       removeEmptyAttributes: true, // 移除空的属性（仅限于原生属性）
       collapseBooleanAttributes: true, // 优化布尔值属性，如：checked="checked" 变为 checked
       removeAttributeQuotes: true, // 移除属性值上的双引号，属性值为多个值时不移除
       minifyCSS: true, // 压缩内嵌式 css 代码（style 标签），只能基本压缩，不能自动添加前缀
       minifyJS: true, // 压缩内嵌式 js 代码（script 标签），只能基本压缩，不能进行转码
       removeStyleLinkTypeAttributes: true, // 移除 style 和 link 标签上的 type 属性
       removeScriptTypeAttributes: true // 移除 script 标签上的 type 属性
     })
     ```

7. del

   - 删除文件目录

   - ```sh
     npm i -D del@6.1.1
     ```

   - ```js
     const del = require('del')
     del(['./dist/']) // 删除 dist 目录
     ```

8. gulp-webserver

   - 启动一个基于 node 书写的服务器

   - ```sh
     npm i -D gulp-webserver
     ```

   - ```js
     const gulpWebserver = require('gulp-webserver')
     gulpWebserver({
       host: 'localhost',
       port: '8080',
       open: './views/login.html', // 默认打开哪一个文件（dist 目录为根目录）
       livereload: true, // 当文件修改的时候，是否自动刷新页面
       proxies: [
         { // 发送 /u 请求，代理到 https://www.escook.cn/api/users
           source: '/u',
           target: 'https://www.escook.cn/api/users'
         },
         { // 发送 /u2/api/users 请求，代理到 https://www.escook.cn/api/users
           source: '/u2',
           target: 'https://www.escook.cn'
         }
       ]
     })
     ```

9. gulp-file-include

   - 在一个 html 页面里面导入一个 html 片段

   - ```sh
     npm i -D gulp-file-include
     ```

   - ```js
     const gulpFileInclude = require('gulp-file-include')
     
     // TODO: 4. 创建一个打包 html 文件的任务
     const htmlHandler = () => {
       return gulp
         .src('./src/views/*.html')
         .pipe(gulpFileInclude({ // 根据配置导入对应的 html 片段
           prefix: '@-@', // 自定义标识符
           basepath: 'src/components' // 基准目录（你的组件文件的目录）
         }))
         .pipe(gulpHtmlmin({
           collapseWhitespace: true,
           removeEmptyAttributes: true,
           collapseBooleanAttributes: true,
           removeAttributeQuotes: true,
           minifyCSS: true,
           minifyJS: true,
           removeStyleLinkTypeAttributes: true,
           removeScriptTypeAttributes: true
         }))
         .pipe(gulp.dest('./dist/views/'))
     }
     ```

   - ```html
     <!-- index.html -->
     
     <!-- 导入头部 -->
     <!-- 语法：自定义标识符 + include('要导入的文件路径', 传递的参数对象) -->
     @-@include('./header.html', { title: '首页' })
     
     <hr>
     
     <div>
       主体内容
     </div>
     
     <hr>
     
     <!-- 导入尾部 -->
     <!-- 语法：自定义标识符 + include('要导入的文件路径', 传递的参数对象) -->
     @-@include('./footer.html', { show: 'active' })
     ```

   - ```html
     <!-- header.html -->
     
     <!-- 使用传递过来的 title 参数，语法：自定义标识 + 符参数名称 -->
     <h2>@-@title</h2>
     ```

   - ```html
     <!-- footer.html -->
     
     <style>
       .active {
         background-color: red;
       }
     </style>
     
     <!-- 使用传递的 show 参数作为值 -->
     <div class="@-@show">页尾</div>
     ```

## 6. 执行一个 gulp 配置好的任务

- 直接打开命令行，切换到 gulpfile.js 所在的目录

- 执行指令 gulp 任务名称

  如：

  ```js
  // gulp 3 的书写语法
  gulp.task('cssHandler', () => { // 任务名称为 cssHandler
    return ...
  })
  // gulp 4 的书写语法
  exports.cssHandler = () => { // 任务名称为 cssHandler
    return ...
  }
  ```

  ```sh
  gulp cssHandler
  ```


## 7. 配置一个默认任务

默认任务的作用就是把所有的任务都给一起执行了。

要么使用 `gulp.series()`，要么使用 `gulp.parallel()`。这两个方法的返回值是一个函数，返回值可以直接被当作任务函数使用。

区别是 `gulp.series()` 开始一个结束一个，`gulp.parallel()` 一起开始一起结束。

```js
exports.default = gulp.parallel(cssHandler, sassHandler, jsHandler, htmlHandler, imgHandler, audioHandler, videoHandler, libHandler, fontsHandler)
```

默认任务为什么一定要叫做 default？

- 因为你使用 gulp 指令的时候应该是 `gulp 任务名称`
- 当你有一个叫做 default 的任务的时候，你可以直接执行指令 `gulp`，它会自动去执行 default 任务

## 8. 利用 gulp 启动一个服务器

- gulp 是基于 node 环境的工具
- node 就是可以做服务器的语言
- gulp 可以启动一个基于 node 的服务器
- 启动服务器，用 dist 目录当做服务器根目录