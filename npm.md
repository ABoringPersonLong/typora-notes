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
