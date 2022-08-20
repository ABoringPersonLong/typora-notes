# 1. 基本示例

index.html 文件：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0">
  <link rel="stylesheet" href="./assets/css/style.css">
  <title>Title</title>
</head>
<body>
<script src="./index.js" type="module"></script>
</body>
</html>
```

index.js 文件：

```js
import * as THREE from 'three' // 导入 three.js
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls.js' // 导入轨道控制器

// 创建场景和相机
const scene = new THREE.Scene() // 创建场景
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000) // 创建相机
camera.position.set(0, 0, 10) // // 设置相机位置 x, y, z
scene.add(camera) // 将相机添加到场景中

// 添加物体
const geometry = new THREE.BoxGeometry(1, 1, 1) // 创建几何体
const material = new THREE.MeshBasicMaterial({color: 175463}) // 创建材质
const cube = new THREE.Mesh(geometry, material) // 创建物体
scene.add(cube) // 将物体添加到场景中

// 设置物体位置
cube.position.set(3, 0, 0) // x, y, z
cube.position.x = 3 // 还可以用属性来设置

// 设置物体缩放
cube.scale.set(3, 2, 1) // x, y, z，当前设置为：宽 3，高 2，长 1
cube.scale.x = 3 // 还可以用属性来设置

// 设置物体旋转
// Math.PI 返回圆周率，旋转 180 度
// 除以 2 就是 90 度
// 除以 3 就是 60 度
// 除以 4 就是 45 度
cube.rotation.set(Math.PI / 4, 0, 0, 'XZY') // x, y, z, 旋转顺序，当前是先旋转 x 轴，再旋转 z 轴，再旋转 y 轴
cube.rotation.x = Math.PI / 4 // 还可以用属性来设置

// 渲染物体
const renderer = new THREE.WebGLRenderer() // 初始化渲染器
renderer.setSize(window.innerWidth, window.innerHeight) // 设置渲染的尺寸大小
document.body.appendChild(renderer.domElement) // 将 webgl 渲染的 canvas 内容添加到 body

// 创建轨道控制器
new OrbitControls(camera, renderer.domElement) // 可以使得相机围绕目标进行轨道运动

// 添加坐标辅助器
const axesHelper = new THREE.AxesHelper(5) // 大小 5
scene.add(axesHelper) // 将坐标辅助添加到场景中

// 渲染每一帧的函数
function render(time) {
	console.log(time) // requestAnimationFrame() 会传递一个参数进来，表示当前这一帧的毫秒值

	// 让物体逐渐往右移动，移动到最大值再变回来
	// cube.position.x += 0.05
	// 优化：在指定时间内移动固定的距离
	const speed = 1 // 速度
	const t = time / 1000 // 当前时间的秒数
	cube.position.x = speed * (t % 5) // 当前的位置 = 速度 * 当前时间（除以 5 是为了在距离大于 5 的使用变回 0 重新走）
	if (cube.position.x >= 5) cube.position.x = 0

	// 让物体旋转
	cube.rotation.x += 0.05

	// 渲染物体
	renderer.render(scene, camera) // 使用渲染器，通过相机将场景渲染进来
	requestAnimationFrame(render) // 浏览器自带的函数，渲染下一帧的时候就会调用 render 函数
}

render()
```

