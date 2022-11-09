# git 的分支操作

```bash
# 创建 login 分支
git checkout -b login

# 提交分支
git add .
git commit -m '完成了登录功能的开发'

# 推送 login 分支
git push -u origin login

# 切换到 master 分支，并合并 login 分支
git checkout master
git merge login

# 删除本地的 login 分支
git branch -d login

# 推送 master 分支
git push
```

# vue 项目打包并生成打包报告

```sh
vue-cli-service build --report
```

# 开启 gzip 配置

使用 `gzip` 可以减小文件体积，使传输速度更快。

可以通过服务器端使用 express 做 gzip 压缩。

安装：

```sh
npm i compression -D
```

使用：

```js
const compression = require('compression')

app.use(compression())
```

# pm2

安装：

```sh
npm i -g pm2
```

使用：

```sh
pm2 start 入口文件路径 --name 自定义名称 # 添加一个新的项目并启动项目
pm2 start ID或自定义名称 # 启动项目
pm2 ls # 查看运行项目
pm2 restart ID或自定义名称 # 重启项目
pm2 stop ID或自定义名称 # 停止项目
pm2 delete ID或自定义名称 # 删除项目
```

# serve

安装：

```bash
npm i -g serve
```

使用：

- serve
- serve -p 3000
- serve ./dist
- serve ./dist -p 3000

# live-server

安装：

```bash
npm i -g live-server
```

使用：

- live-server
- live-server --port=8080
- live-server ./dist
- live-server ./dist --port=8080

# aos

安装：

```bash
npm i aos
```

导入：

```html
<!-- 导入样式 -->
<link rel="stylesheet" href="bower_components/aos/dist/aos.css"/>
<!-- 导入脚本 -->
<script src="bower_components/aos/dist/aos.js"></script>

<script>
  AOS.init() // 初始化 aos
</script>
```

使用：

```html
<!-- zoom-in：从右往左移动 -->
<!-- zoom-out 从左往右移动 -->
<!-- aos-duration：持续时间 -->
<div data-aos="zoom-in" aos-duration="1000">
  <h1>this sssssss</h1>
  <p>gdfg dgdfgdf</p>
</div>
```
