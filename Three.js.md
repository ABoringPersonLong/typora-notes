# 1. 引入 three.js

## 1. script 标签方式引入 three.js

你可以像平时开发 web **前端**项目一样，把 three.js 当做一个 js 库引入你的项目。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0">
  <script src="./three.js-dev/build/three.min.js"></script>
  <title>Title</title>
</head>
<body>
<script>
  console.log(THREE)
</script>
</body>
</html>
```

## 2. es6 的 import 方式引入

给 script 标签设置`type="module"`，也可以在 .html 文件中使用`import`方式引入 three.js。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0">
  <title>Title</title>
</head>
<body>
<script type="module">
  import * as THREE from './three.js-dev/build/three.module.js'
  console.log(THREE)
</script>
</body>
</html>
```

## 3. three.js 工程化开发

平时学习，为了方便可以直接在 .html 文件中引入 three.js 相关文件，不过在正式开发的时候，你可以在你的 node.js 工程文件中，通过 npm 命令安装 three.js。

安装特定版本的 three.js：

```bash
npm i three@0.143.0
```

使用：

```js
// 引入 three.js
import * as THREE from 'three'
console.log(THREE)

// 引入扩展库
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls.js'
console.log(OrbitControls)
```

# 2. 第一个 3D 案例

## 1. 创建 3D 场景

**三维场景`Scene`**

你可以将`Scene`理解为虚拟的 3D 场景，用来表示模拟生活中的真实三维场景，或者说三维世界。

```js
const scene = new THREE.Scene() // 创建 3D 场景对象 Scene
```























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
<script src="./01-基本示例.js" type="module"></script>
</body>
</html>
```

01-基本示例.js 文件：

```js
import * as THREE from 'three' // 导入 three.js
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls.js' // 导入轨道控制器

// 创建场景和相机
const scene = new THREE.Scene() // 创建场景
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000) // 创建相机
camera.position.set(0, 0, 10) // 设置相机位置 x, y, z
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
const controls = new OrbitControls(camera, renderer.domElement) // 可以使得相机围绕目标进行轨道运动
controls.enableDamping = true // 启动控制器阻尼（惯性），让控制器更有真实效果，必须在动画循环里调用 controls.update()

// 添加坐标辅助器
const axesHelper = new THREE.AxesHelper(5) // 大小 5
scene.add(axesHelper) // 将坐标辅助添加到场景中

// 设置时钟
const clock = new THREE.Clock()

// 渲染每一帧的函数
function render(time) {
	// 让物体逐渐往右移动，移动到最大值再变回来
	// cube.position.x += 0.05
	// if (cube.position.x >= 5) cube.position.x = 0
	// 优化：在指定时间内移动固定的距离
	// console.log(time) // requestAnimationFrame() 会传递一个参数进来，表示当前这一帧的毫秒值
	// const speed = 1 // 速度
	// const t = time / 1000 // 当前时间的秒数
	// cube.position.x = (speed * t) % 5 // 当前的位置 = 速度 * 当前时间（除以 5 是为了在距离大于 5 的使用变回 0 重新走）
	// 再优化：设置时钟
	const deltaTime = clock.getDelta()
	console.log('两次获取时间的间隔', deltaTime)
	const time2 = clock.getElapsedTime()
	console.log('时钟运行的总时长', time2)
	const speed = 1 // 速度
	cube.position.x = (speed * time2) % 5

	// 让物体旋转
	cube.rotation.x += 0.05

	// 渲染物体
	controls.update()
	renderer.render(scene, camera) // 使用渲染器，通过相机将场景渲染进来
	requestAnimationFrame(render) // 浏览器自带的函数，渲染下一帧的时候就会调用 render 函数
}

render()
```

# 2. 使用 gsap 设置各种动画效果

安装：

```bash
npm i gsap
```

02-gsap.js 文件：

```js
import * as THREE from 'three'
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls.js'
import gsap from 'gsap' // 导入动画库

const scene = new THREE.Scene()
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
camera.position.set(0, 0, 10)
scene.add(camera)

const geometry = new THREE.BoxGeometry(1, 1, 1)
const material = new THREE.MeshBasicMaterial({color: 175463})
const cube = new THREE.Mesh(geometry, material)
scene.add(cube)

const renderer = new THREE.WebGLRenderer()
renderer.setSize(window.innerWidth, window.innerHeight)
document.body.appendChild(renderer.domElement)

const controls = new OrbitControls(camera, renderer.domElement)
controls.enableDamping = true

const axesHelper = new THREE.AxesHelper(5)
scene.add(axesHelper)

// 控制 cube.position
const animate1 = gsap.to(cube.position, {
	x: 5, // 将 x 位置改成 5
	duration: 3, // 花费 3 秒
	ease: 'power1.inOut', // 速度，power1.inOut 表示先慢再快
	// repeat: 2, // 执行完后，再重复 2 次
	repeat: -1, // 重复无限次
	yoyo: true, // 往返运动
	delay: 2, // 延迟 2 秒
	onStart() { // 动画开始的回调函数
		console.log('动画开始')
	},
	onComplete() { // 动画完成的回调函数
		console.log('动画完成')
	}
})

// 控制 cube.rotation
gsap.to(cube.rotation, {
	x: Math.PI * 2, // 将 x 位置旋转 360 度
	duration: 2, // 花费 2 秒
	ease: 'none' // 匀速
})

function render() {
	controls.update()
	renderer.render(scene, camera)
	requestAnimationFrame(render)
}

render()

// 双击暂停/开始动画
window.addEventListener('dblclick', () => {
	if (animate1.isActive()) animate1.pause() // 如果动画正在运动，暂停动画
	else animate1.resume() // 如果动画已经暂停，恢复动画
})

// 监听屏幕尺寸变化，更新渲染画面
window.addEventListener('resize', () => {
	camera.aspect = window.innerWidth / window.innerHeight // 更新摄像头
	camera.updateProjectionMatrix() // 更新摄像机的投影柜阵
	renderer.setSize(window.innerWidth, window.innerHeight) // 更新渲染器的尺寸大小
	renderer.setPixelRatio(window.devicePixelRatio) // 设置渲染器的像素比
})

// 按下 Q 键进入/退出全屏
window.addEventListener('keyup', event => {
	if (event.code === 'KeyQ') {
		if (!document.fullscreenElement) renderer.domElement.requestFullscreen()
		else document.exitFullscreen()
	}
})
```

# 3. 使用 dat.gui 改变属性

安装：

```bash
npm i dat.gui
```

03-dat.gui.js 文件：

```js
import * as THREE from 'three'
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls.js'
import gsap from 'gsap' // 导入动画库
import * as dat from 'dat.gui' // 导入 dat.gui

const scene = new THREE.Scene()
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
camera.position.set(0, 0, 10)
scene.add(camera)

const geometry = new THREE.BoxGeometry(1, 1, 1)
const material = new THREE.MeshBasicMaterial({color: 175463})
const cube = new THREE.Mesh(geometry, material)
scene.add(cube)

const gui = new dat.GUI() // 创建 gui

// 修改物体的属性
gui
	.add(cube.position, 'x') // 改变 cube.position 对象里的 x 属性
	.min(0) // 最小 0
	.max(5) // 最大 5
	.step(0.01) // 步长 0.01
	.name('移动x轴坐标') // 设置标题名称，如果没有设置，则默认就是上面指定的 x
	.onChange(value => console.log('值被修改了', value)) // 监听值被改变，每次移动的过程中也会一直执行
	.onFinishChange(value => console.log('移动停止，值被修改了', value)) // 监听值被改变，只有停止移动后才执行

// 修改物体的颜色
gui
	.addColor({color: '#ffff00'}, 'color') // 改变第一个参数对象里的 color 属性
	.name('颜色') // 设置标题名称，如果没有设置，则默认就是上面指定的 color
	.onChange(value => { // 监听值被改变
		console.log('颜色被修改了', value)
		cube.material.color.set(value) // 每次改变设置物体的材质颜色
	})

// 修改物体的布尔值属性
gui.add(cube, 'visible').name('是否显示') // 改变 cube 对象里的 visible 属性，该属性是个布尔值，用于控制物体的显示和隐藏

// 设置点击按钮执行某个函数
gui.add({ fn: () => gsap.to(cube.position, {x: 5, duration: 3, ease: 'power1.inOut', repeat: -1, yoyo: true}) }, 'fn')

// 添加文件夹
const folder = gui.addFolder('设置立方体')
// 在文件夹里添加控制项，就像是 gui.add()
folder.add(cube.material, 'wireframe').name('是否显示线框') // wireframe 属性表示是否显示线框

const renderer = new THREE.WebGLRenderer()
renderer.setSize(window.innerWidth, window.innerHeight)
document.body.appendChild(renderer.domElement)

const controls = new OrbitControls(camera, renderer.domElement)
controls.enableDamping = true

const axesHelper = new THREE.AxesHelper(5)
scene.add(axesHelper)

function render() {
	controls.update()
	renderer.render(scene, camera)
	requestAnimationFrame(render)
}

render()

window.addEventListener('resize', () => {
	camera.aspect = window.innerWidth / window.innerHeight
	camera.updateProjectionMatrix()
	renderer.setSize(window.innerWidth, window.innerHeight)
	renderer.setPixelRatio(window.devicePixelRatio)
})
```

# 4. 立方缓冲几何体

04-立方缓冲几何体.js 文件：

```js

```

