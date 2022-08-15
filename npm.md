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

