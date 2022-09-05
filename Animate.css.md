# 1. 引入 Animate.css

## 1. 通过 SDN 引入

```html
<!-- 本地引入 -->
<link rel="stylesheet" href="./lib/animate.min.css">

<!-- 网络引入 -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css">
```

## 2. 通过 npm 安装

安装：

```sh
npm i animate.css
```

导入：

```js
import 'animate.css'
```

# 2. 基本用法

## 第一种方式：添加类名

将类 `animate__animated` 与任何**动画名称**一起添加到元素（动画名称不要忘记加 `animate__` 前缀！），因为 `animate__animated` 类中设置了动画持续时间：

```html
<div class="animate__animated animate__bounce">An animated element</div>
```

## 第二种方式：使用 animation

html：

```html
<div class="box">An animated element</div>
```

css：

```css
.box {
  animation: bounce;
  animation-duration: 1s;
}
```

