```
    4.DOM：
      1.DOM简单学习：为了满足案列要求
	      功能：控制html文档的内容
	      代码：获取页面标签(元素)对象 Element
	        document.getElementById("id值");获取指定id的标签对象
	      操作Element对象：
	            1.获取属性值
	                var a = document.getElementById("a");
	                var value = a.src;
	            2.修改属性值：
	                var a = document.getElementById("a");
	                a.src = "./b.png";
	            3.修改标签体内容：
	                var b = document.getElementById("b");
                    b.innerHTML = "修改后的内容";
      2.事件简单学习
            功能：
                某些组件被执行了某些操作后，触发某些代码的执行
            如何判定事件：
                1.直接在html标签上，指定事件的属性(操作)，属性值就是js代码
                    1.事件：
                        onclick：单击事件
                2.通过js获取元素对象，指定事件属性，设置一个函数
      3.概念：Document Object Model 文档对象模型
            将标记语言文档的各个组成部分，封装为对象。可以使用这些对象，对标记语言文档进行CRUD的动态操作
      4.W3C DOM 标准被分为 3 个不同的部分：
            1.核心 DOM：针对任何结构化文档的标准模型
                Document：文档对象
                  1.创建(获取)：在html dom模型中可以使用Window对象来获取
                        第一种：Window.document
	                    第二种：document
	                2.属性
	                  document.referrer：获取跳转到这个页面的 url（例如：从 http://localhost/aaa 跳转到 http://localhost/bbb，获取到的就是 http://localhost/aaa）
	                3.方法
	                    1.获取 Element 对象：
	                        getElementById()：根据id属性值获取指定元素对象
	                        getElementsByTagName()：根据元素名称获取所有元素对象，返回一个数组
	                        getElementsByClassName()：根据class属性值获取所有元素对象，返回一个数组
	                        getElementsByName()：根据name属性值获取所有元素对象，返回一个数组
	                        querySelector(选择器)：根据 css 选择器获取指定的元素对象
	                        querySelectorAll(选择器)：根据 css 选择器获取所有的元素对象，返回一个数组
						2.获取 html 和 body 对象：
							document.documentElement：获取 html 元素对象
							document.body：获取 body 元素对象
	                    3.创建其他 DOM 对象：
	                        createAttribute(name)
	                        createComment()
	                        createElement()：创建一个html元素
	                        createTextNode()
                Element元素对象
                    1.获取(创建)：
                        通过document来获取和创建
                    2.属性
                      dataset：访问元素上设置的所有自定义属性
                    3.方法
                        setAttribute()：设置属性
                        removeAttribute()：删除属性
                Attribute：属性对象
                Text：文本对象
                Comment：注释对象
                Node：节点对象，其他5个对象的父对象
                    特点：所有DOM对象都可以被认为是一个节点
                    方法：
                        CRUD DOM树：
                            appendChild()：向节点的子节点列表的结尾添加新的子节点
                            removeChild()：删除(并返回)当前节点的指定子节点
                            replaceChild()：用新节点替换一个子节点
                    属性：
                        parentNode：返回节点的父节点
                        firstChild：返回节点的第一个子节点，包含元素节点和文本节点
                        firstElementChild：返回节点的第一个子元素节点，IE9 以上才支持
                        lastChild：返回节点的最后一个子节点，包含元素节点和文本节点
                        lastElementChild：返回节点的最后一个子元素节点，IE9 以上才支持
                        childNodes：返回节点的所有子节点，包含元素节点和文本节点
                        children：返回所有的子元素节点
                        previousSibling：返回节点的上一个兄弟元素节点，包含元素节点和文本节点
                        previousElementSibling：返回节点的上一个兄弟元素节点
                        nextSibling：返回节点的下一个兄弟元素节点，包含元素节点和文本节点
                        nextElementSibling：返回节点的下一个兄弟元素节点
            2.XML DOM：针对 XML 文档的标准模型
            3.HTML DOM： 针对 HTML 文档的标准模型
                1.标签体的设置和获取：innerHTML
                    var a = document.getElementById("a");
                    a.innerHTML = "修改后的内容";
                    a.innerHTML += "添加的内容";
                2.使用html元素对象的属性
                3.控制样式
            注意：
                this 代表当前标签
                实现：href="javascript:void(0);"// 相当于注销掉href
        5.事件监听机制
            1.概念：某些组件被执行了某些操作后，触发某些代码的执行
                事件：某些操作。如：单击、双击、键盘按下、鼠标移动
                事件源：某些组件。如：按钮、文本输入框...
                监听器：执行某些代码。
                注册监听：将事件、事件源、监听器结合在一起。但事件源上发生了某个事件，则触发执行某个监听器代码。
            2.常见的事件：
                1.点击事件：
                    onclick: 鼠标点击左键触发
                    ondblclick：双击事件
                2.焦点事件：
                    onblur：失去焦点
                        用于表单校验
                        用于表单校验
                    onfocus：元素获得焦点
                        onfocus="this.blur();"：一获得焦点就失去焦点，也就是让元素不能获得焦点
                3.加载事件：
                    onload：一张页面或一副图像完成加载
                        可以给<body>、window、image用
                4.鼠标事件：
                    onmousedown：鼠标按键被按下
                        此事件在调用方法时会传一个 event 对象，方法接收后可以通过 event 的属性 button
                        来获取是鼠标那个键被按下
                        左键0、滚轮1、右键2、上一页3、下一页4
                    onmouseup：鼠标按键被松开
                    onmousemove：鼠标被移动
                    onmouseover：鼠标经过触发
					onmouseout：鼠标离开触发
                    onscroll：鼠标滚动条滚动触发
                5.键盘事件：
                    onkeydown：某个键盘按键被按下
                        此事件在调用方法时会传一个 event 对象，方法接收后可以通过 event 的属性 keyCode
                        获取是键盘那个键被按下
                    onkeyup：某个键盘按键被松开
                        同理
                    onkeypress：某个键盘按键被按下并松开
                        同理
                6.选择和改变：
                    onchange：域的内容被改变
                    onselect：文本被选中
                7.表单事件：
                    onsubmit：确认按钮被点击
                    onreset：重置按钮被点击
            6.DOM 完整的解析过程：
              1.解析 HTML 结构
              2.加载外部脚本和样式表文件
              3.解析并执行脚本代码 // js 之类的
              4.DOM 树构建完成 // 触发 DOMContentLoaded 事件
              5.加载图片等外部文件
              6.页面加载完毕 // 触发 load 事件
		6.事件高级：
			1.注册事件(绑定事件):
				给元素添加事件, 称为注册事件或者绑定事件
				注册事件有两种方式: 传统方式和方法
				1.传统注册方式:
					利用 on 开头的事件:
						<button onclick="alert('HelloWorld')"></button>
						btn.onclick = function () {}
					特点:
						注册事件的唯一性
						同一个元素同一个事件只能设置一个处理行数, 最后注册的处理函数将会覆盖前面注册的处理函数
				2.方法监听注册方式:
					w3c 标准推荐方式:
						eventTarget.addEventListener(type, listener[, useCapture]);
						addEventListener(): 它是一个方法
						IE9 之前的 IE 不支持此方法, 可使用 attachEvent() 代替
					特点:
						同一个元素同一个事件可以注册多个监听器
					addEventListener 方式:
						eventTarget.addEventListener() 方法将指定的监听器注册到 eventTarget(目标对象)上, 当该对像触发指定的事件时, 就会执行事件处理函数
						该方法接收三个参数:
							type: 事件类型字符串, 比如 click, mouseover 注意这里不要带 on
							listener: 事件处理函数, 事件发生时, 会调用该监听函数
							useCapture: 可选参数, 是一个布尔值, 默认是 false
			2.删除事件(解绑事件):
				1.传统注册方式::
					eventTarget.onclick = null;
				2.方法监听注册方式:
					eventTarget.removeEventListener(type, listener[, useCapture]);
			3.DOM 事件流:
				事件流描述的是从页面中接收事件的顺序
				事件发生时会在元素节点之间按照特定的顺序传播, 这个转播过程即 DOM 事件流
				DOM 事件流分为 3 个阶段:
					1.捕获阶段
					2.当前目标阶段
					3.冒泡阶段
					事件冒泡: IE 最早提出, 事件开始时由最具体的元素接收, 然后逐级向上传播到 DOM 最顶层节点的过程
					事件捕获: 网景最早提出, 由 DOM 最顶层节点开始, 然后逐级向下传播到最具体的元素接收的过程
				注意:
					1.js 代码中只能执行捕获或者冒泡其中的一个阶段
					2.onclick 和 attachEvent 只能得到冒泡阶段
					3.addEventListener(type, listener[, useCapture]) 第三个参数默认是 false, 如果是 true, 表示在事件捕获阶段调用事件处理程序, 反之表示在事件冒泡阶段调用事件处理程序
					4.实际开发中我们很少使用事件捕获, 我们更关注事件冒泡
					5.有些事件是没有冒泡的, 比如 onblur, onfocus, onmouseenter, onmouseleave
					6.事件冒泡有时候会带来麻烦, 有时候又会帮助很巧妙的做某些事件
			4.事件对象:
				事件调用的函数里面加个形参 event, 这个 event 就是事件对象
				1.官方解释:
					event 对象代表事件的状态, 比如键盘按键的状态、 鼠标的位置、 鼠标按钮的状态
				2.简单解释:
					事件发生后, 根事件相关的一系列信息数据的集合都放到这个对象里面, 这个对象就是事件对象 event, 它有很多属性和方法
					比如:
						谁绑定了这个事件
						鼠标触发事件的话, 会得到鼠标的相关信息, 如鼠标位置
				3.使用语法:
					这个 event 是个形参, 系统帮我们设定为事件对象, 不需要传递实参过去
					当我们注册事件时, event 对象就会被系统自动创建, 并依次传递给事件监听器 (事件处理函数)
				4.事件对象的兼容性方案:
					事件对象本身的获取存在兼容问题:
						1.标准浏览器中是浏览器给方法传递的参数, 只需要定义形参 event 就可以获取到
						2.在 IE678 中, 浏览器不会给方法传递参数, 如果需要的话, 需要到 window.event 中获取
					解决:
						event = event || window.event
				5.事件对象的常见属性和方法:
					target: 返回触发事件的对象, 标准
                        target 返回的是触发事件的对象 (元素), this 返回的是绑定事件的对象 (元素)
                        区别: target 点击了哪个元素, 就返回那个元素，this 哪个元素绑定了这个点击事件，那么就返回谁
					srcElement: 返回触发事件的对象, 非标准 IE678 使用
					type: 返回事件的类型, 比如 click, mouseover 不带 on
					cancelBubble: 该属性阻止冒泡, 非标准 IE678 使用
					returnValue: 该属性默认事件(默认行为), 非标准 IE678 使用, 比如不然链接跳转
					preventDefault(): 该方法阻止默认事件(默认行为), 标准, 比如不让链接跳转
					stopPropagation(): 阻止冒泡, 标准
			5.阻止事件冒泡:
				事件冒泡: 开始时由最具体的元素接收是, 然后逐级向上传播到 DOM 最顶层节点
				事件冒泡本身的特性, 会带来的坏处, 也会带来的好处, 需要我们灵活掌握
				阻止事件冒泡:
					标准写法:
						利用事件对象里面的 stopPropagation() 方法
					非标准写法:
						IE678 利用事件对象 cancelBubble 属性
			6.事件委托(代理、 委派):
				1.事件委托:
					事件委托也称为事件代理, 在 jQuery 里面称为事件委派
				2.事件委托的原理:
					不是每个子节点单独设置事件监听器, 而是事件监听器设置在其父节点上, 然后利用冒泡原理影响设置每个子节点
				3.事件委托的作用:
					我们只操作了一次 DOM, 提高了程序的性能
			7.常用的鼠标事件:
				onclick: 鼠标点击左键触发
				onmouseover: 鼠标经过触发
				onmouseout: 鼠标离开触发
				onfocus: 获得焦点触发
				onblur: 失去焦点触发
				onmousemove: 鼠标移动触发
				onmouseup: 鼠标按键被松开触发
				onmousedown: 鼠标按键被按下触发
				onscroll: 鼠标滚动条滚动触发
				contextmenu: 鼠标右键菜单
					禁止鼠标右键菜单: event.preventDefault();
				selectstart: 鼠标选中文字
					禁止鼠标选中文字: event.preventDefault();
				鼠标事件对象:
					event 对象代表事件的状态, 根事件相关的一系列信息的集合. 现阶段我们主要是用鼠标事件对象
					MouseEvent 和键盘事件对象 KeyboardEvent
					鼠标事件对象属性:
					  offsetX: 返回鼠标相对于当前元素的 x 坐标
					  offsetY: 返回鼠标相对于当前元素的 y 坐标
						clientX: 返回鼠标相对于浏览器窗口可视区的 x 坐标
						clientY: 返回鼠标相对于浏览器窗口可视区的 y 坐标
						pageX: 返回鼠标相对于文档页面的 x 坐标 IE9+ 支持
						pageY: 返回鼠标相对于文档页面的 y 坐标 IE9+ 支持
						screenX: 返回鼠标相对于电脑屏幕的 x 坐标
						screenY: 返回鼠标相对于电脑屏幕的 y 坐标
				鼠标拖动：
				  dragstart：开始拖动
				  dragover：拖到上面
				  dragend：结束拖动
				  使用鼠标拖动事件需要在元素上加 draggable="true" 表示让元素可拖动
			8.常用的键盘事件:
				onkeyup: 某个键盘按键被松开时触发
				onkeydown: 某个键盘按键被按下时触发
				onkeypress: 某个键盘按键被按下并松开时触发, 不识别功能键, 比如: ctrl、 shift、 箭头等
				三个事件的执行顺序 keydown -> keypress - keyup
				键盘事件对象属性:
					keyCode: 返回该键的 ASCII 值
					注意:
						onkeydown 和 onkeyup 不区分字母大小写, onkeypress 区分字母大小写
						在我们实际开发中, 我们更多的使用 keydown 和 keyup, 它能识别所有的键(包括功能键)
						keypress 不识别功能键, 但是 keyCode 属性能区分大小写, 返回不同的 ASCII 值
			9.其他事件:
				ontransitionend	过渡完成之后触发
	3.BOM：
	    1.概述:
			BOM (Browser Object Model) 浏览器对象模型, 它提供了独立于内容而与浏览器窗口进行交互的对象, 其核心对象是 window
			BOM 由一系列相关的对象构成, 并且每个对象都提供了很多方法与属性
			BOM 缺乏标准, JavaScript 语法的标准化组织是 ECMA, DOM 的标准化组织是 W3C, Bom 最初是 Netscape 浏览器标准的一部分
			BOM 的构成:
				BOM 比 DOM 更大, 它包含 DOM
				结构:
					window
					document - location - navigation - screen - history
				window 对象是浏览器的顶级对象, 它具有双重角色
					1.它是 js 访问浏览器窗口的一个接口
					2.它是一个全局对象, 定义在全局作用域中的变量、 函数都会变成 window 对象的属性和方法
					在调用的时候可以省略 window, 前面学习的对话框都属于 window 对象方法, 如 alert()、 prompt() 等
					注意: window 下的一个特殊属性 window.name, 定义变量时尽量不要叫 name
		2.window 对象的常见事件:
			onload: 窗口加载事件, 是窗口 (页面) 加载事件, 当文档内容完全加载完成会触发该事件 (包括图像、 脚本文件、 CSS 文件等), 就调用的处理函数
			onresize: 调整窗口大小事件, 是调整窗口大小加载事件, 当触发时就吊桶的处理函数
				注意:
					1.只要窗口大小发生像素变化, 就会触发这个事件
					2.我们经常利用这个事件完成响应式布局, window.innerWidth 当前屏幕的宽度
	    3.由5个对象组成：
	        Window: 窗口对象
	            1.创建
	                无需创建
	            2.方法
	                1.与弹出框有关的方法：
	                    alert()：显示带有一段消息和一个确认按钮的警告框
	                    confirm()：显示带有一段消息以及确认按钮和取消按钮的对话框
	                        点击确认返回true
	                        点击取消返回false
	                    prompt()：显示可提示用户输入的对话框
	                        返回输入的值
	                2.与开发关闭有关的方法：
	                    open()：打开一个新的浏览器窗口，返回值是该窗口的Window对象
	                    close()：关闭浏览器窗口，谁调用的就关谁
	                3.与定时器有关的方法：
	                    setTimeout()：在指定的毫秒数后调用函数或计算机表达式(只执行一次)
	                        第一个参数：js代码或者方法对象
	                        第二个参数：毫秒值
	                        返回值：返回一个唯一编号，用于取消这个定时器
	                    clearTimeout()：取消由 setTimeout() 方法设置的 timeout
	                    setInterval()：在指定的毫秒数后调用函数或计算机表达式(循环执行)
	                        第一个参数：js代码或者方法对象
	                        第二个参数：毫秒值
	                        返回值：返回一个唯一编号，用于取消这个定时器
	                    clearInterval()：取消由 setInterval() 方法设置的 timeout
	                4.其他方法：
	                    print()：打印
	            3.属性
	                navigator：获取浏览器对象
	                screen：获取显示器屏幕对象
	                history：获取历史记录对象
	                location：获取地址栏对象
	                document：获取document对象
	                screen：获取设备宽高
	                localStorage：获取本地存储器对象，相当于 Cookie
                        setItem(key, value)：存储键值对
                        getItem(key)：获取指定键的值
                        removeItem(key)：删除指定键
                        clear()：全部清除
                        key(index)：获取指定下标的键
                        length：获取键值对的数量
	            4.特点
	                1.Window对象不需要创建可以直接使用'window.方法名();'调用，也可以省略window直接用'方法名();'
	            5.在控制台输出：console.log("Hello World");
	        Screen: 显示器屏幕对象(不学)
	        Location: 地址栏对象
	            1.创建(获取)
	                第一种：Window.location
	                第二种：location
	            2.属性
	            		href：修改url地址，有历史记录
	            3.方法
	                reload(): 重新加载当前文档 (刷新)
	                assign：跳转到新的url地址，有历史记录
                  replace：重定向到新的url地址，没有历史记录
                  reload：重新加载当前页面
					assign(): 根 href 一样, 可以跳转页面 (也称为重定向页面)
					replace(): 替换当前页面, 因为不记录历史, 所以不能后退页面
	            3.属性
	                host：设置或返回主机名和当前 URL 的端口号
                    hostname：设置或返回当前 URL 的主机名
                    href：设置或返回完整的 URL
                    pathname：设置或返回当前 URL 的路径部分
                    port：设置或返回当前 URL 的端口号
                    protocol：设置或返回当前 URL 的协议
                    search：设置或返回从 ? 开始的 URL
			Navigator: 浏览器对象
				navigator 对象包含有关浏览器的信息, 它由很多属性, 我们最常用的式 userAgent, 该属性可以返回由客户发送服务器的 user-agent 头部的值
				下面前端代码可以判断用户是用那个终端打开的页面, 实现跳转:
					<script>
						if ((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
							window.location.href = "./移动.html";// 如果是用手机访问的这个页面就跳转到移动端的页面
						}
					</script>
					判断是否是苹果手机：
						console.log(navigator.userAgent.includes('iPhone'))
	        History: 历史记录对象
	            1.创建 (获取):
	                第一种：Window.history
	                第二种：history
	            2.方法:
	                back(): 加载 history 列表中的前一个 url
	                forward(): 加载 history 列表中的下一个 url
	                go(参数): 加载 history 列表中的某个具体页面, 如果是 1 前进 1 个页面, 如果是 -1 后退 1 个页面
	            3.属性:
	                length：返回当前窗口的历史记录个数
    4.其他方法：
        toFixed(2): 四舍五入，保留两位小数
		trim(): 用于删除字符串的头尾空白符, 空白符包括: 空格、 制表符 (tab)、 换行符等其他空白符等
3.PC端网页特效:
	1.元素偏移量 offset 系列:
		offset 翻译过来就是偏移量, 我们使用 offset 系列相关属性可以动态的得到该元素的位置 (偏移)、 大小等
			获取元素距离带有定位父元素的位置
			获取元素自身的大小 (宽度高度)
			注意: 返回的数值都不带单位
		offset 系列属性:
			element.offsetParent: 返回作为该元素带有定位的父级元素, 如果父级都没有定位则返回 body
			element.offsetTop: 返回元素与带有定位的父元素上方的距离, 如果父级都没有定位则返回与 body 的距离
			element.offsetLeft: 返回元素与带有定位的父元素左边的距离, 如果父级都没有定位则返回与 body 的距离
			element.offsetWidth: 返回自身包括 padding、 边框、 内容区的宽度, 返回数值不带单位
			element.offsetHeight: 返回自身包括 padding、 边框、 内容区的高度, 返回数值不带单位
		offset 与 style 的区别:
			offset 可以得到任意样式表中的样式值                            style 只能得到行内样式表中的样式值
			offset 系列获得的数值是没有单位的                              style.width 获得的是带有单位的字符串
			offsetWidth 包含 padding + border + width                    style.width 获得不包含 padding 和 border 的值
			offsetWidth 等属性是只读属性, 只能获取不能赋值                  style.width 是可读写属性, 可以获取也可以赋值
			所以, 我们想要获取元素大小位置, 用 offset 更合适                所以, 我们想要给元素更改值, 则需要用 style 改变
	2.元素可视区 client 系列:
		client 翻译过来就是客户端, 我们使用 client 系列相关属性来获取元素可视区的相关信息
			通过 client 系列的相关属性可以动态的得到该院的边框大小、 元素大小等
		client 系列属性:
			element.clientTop: 返回元素上边框的大小
			element.clientLeft: 返回元素左边框的大小
			element.clientWidth: 返回自身包括 padding、 内容区的宽度, 不含边框, 返回数值不带单位
			element.clientHeight: 返回自身包括 padding、 内容区的高度, 不含边框, 返回数值不带单位
		window 对象获取可见区域的宽高的方式：
		  innerWidth：文档显示区域的宽度，不包括工具栏等，IE9+支持
		  innerHeight：文档显示区域的高度，不包括工具栏等，IE9+支持
	3.立即执行函数:
		(function () {})()
		主要作用: 创建一个独立的作用域
	4.元素滚动 scroll 系列:
		scroll 翻译过来就是滚动, 我们使用 scroll 系列的相关属性可以动态的得到该元素的大小、 滚动距离等
		scroll 系列属性:
			element.scrollTop: 返回被卷去的上侧距离, 返回数值不带单位
			element.scrollLeft: 返回被卷去的左侧距离, 返回数值不带单位
			element.scrollWidth: 返回自身实际的宽度, 不含边框, 返回数值不带单位
			element.scrollHeight: 返回自身实际的高度, 不含边框, 返回数值不带单位
			window.scroll(x, y): 滚动窗口至文档中的特定位置
		页面被卷去部分的宽高:
			window.pageYOffset: 页面被卷去的头部, 返回被卷去上侧距离, 返回数值不带单位
			window.pageXOffset: 页面被卷去的左侧, 返回被卷去左侧距离, 返回数值不带单位
		页面被卷去部分兼容性解决方案:
			function getScroll() {
				return {
					left: window.pageXOffset || document.documentElement.scrollLeft || document.body.scrollLeft || 0,
					top: window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0
				};
			}
			使用: getScroll().left; 和 getScroll().top;
	5.三大系列总结:
		1.offset 系列经常用于获得元素位置 offsetLeft offsetTop
		2.client 系列经常用于获取元素大小 clientWidth clientHeight
		3.scroll 系列经常获取滚动距离 scrollLeft scrollTop
	6.mouseover 和 mouseenter 的区别:
		mouseover 鼠标经过自身盒子会触发, 经过子盒子还会触发
		mouseenter 鼠标只会经过自身盒子触发
		之所以这样, 就是因为 mouseenter 不会冒泡
		根 mouseenter 搭配的鼠标离开事件 mouseleave 同样不会冒泡
 	7.动画函数封装:
		核心原理: 通过定时器 setInterval() 不断移动盒子位置
		实现步骤:
			1.获取盒子当前位置
			2.让盒子在当前位置加上 1px 的距离
			3.利用定时器不断重复这个操作
			4.加一个结束定时器的条件
			5.注意此元素需要添加定位, 才能使用 element.style.left
4.移动端网页特效:
	1.触屏事件:
		1.概述:
			移动端浏览器兼容性较好, 我们不需考虑以前 js 的兼容性问题, 可以放心的使用原生 js 书写效果, 但是移动端也有自己独特的地方. 比如触屏事件 touch (也称触摸事件), Android 和 IOS 都有.
			touch 对象代表一个触摸点. 触摸点可能是一根手指, 也可能是一根触摸笔. 屏幕事件可响应用户手指 (或触控笔) 对屏幕或者触控板操作.
		2.常见的触屏事件如下:
			touchstart: 手指在一个 DOM 元素上按住时触发
			touchmove: 手指在一个 DOM 元素上按住并滑动时触发
			touchend: 手指在一个 DOM 元素上松开时触发
			触摸事件对象 (TouchEvent):
				TouchEvent 是一类描述手指在触摸平面 (触摸屏、 触摸板等) 的状态变化的事件. 这类事件用于描述一个或多个触点, 是开发者可以检测触点的移动, 触点的增加和减少, 等等
				触摸事件对象重点看三个常见对象列表:
					touches: 正在触摸屏幕的所有手指的一个列表
					targetTouches: 正在触摸当前 DOM 元素上的手指的一个列表
					changedTouches: 手指状态发生了改变的列表, 从无到有, 从有到无变化
	2.移动端常见特效:
		classList 属性:
			classList 属性是 H5 新增的一个属性, 返回元素的类名, 但是 IE10 以上版本支持
			add(): 添加类
			remove(): 删除类
			toggle: 切换类
		案例1: 移动端拖动元素
		案例2: 移动端轮播图
		案例3: 返回顶部
	3.移动端常用开发插件:
		fastclick 插件:
			移动端 click 事件会有 300ms 的延时, 原因是移动端屏幕双击会缩放 (double tap to zoom) 页面
			使用 meta 标签解决 300ms 延时:
				<meta name="viewport" content="user-scalable=no">
			使用插件, fastclick 插件解决 300ms 延时:
				移动端要求的是快速开发, 所以我们经常会借助于一些插件来帮我们呢完成操作, 那么什么是插件呢？
				js 插件是 js文件, 它遵循一定规范编写, 方便程序展示效果, 拥有特定功能且方便调用, 如轮播图和瀑布流插件
				特点: 它一般是为了解决某个问题而专门存在, 其功能单一, 并且比较小
				我们以前写的 animate.js 也算一个最简单的插件
				fastclick 插件解决 300ms 延时, 使用延时
				gethub 官网地址: https://github.com/ftlabs/fastclick
		swiper 插件:
			中文官网地址: https://www.swiper.com.cn/
		superslide 插件:
			官网地址: http://www.superslide2.com/
		iscroll 插件:
			gethub 官网地址: https://github.com/cubiq/iscroll
		插件的使用总结:
			1.确认插件实现的功能
			2.去官网查看使用说明
			3.下载插件
			4.打开 demo 实例文件, 插件需要引入的相关文件, 并且引入
			5.复制 demo 实例文件中的结构 html, 样式 css 以及 js 代码
		练习-移动端视频插件 zy.media.js:
			H5 给我们提供了 video 标签, 但是浏览器的支持情况不同
			不同的视频格式文件, 我们可以通过 source 解决
			但是外观样式, 还有暂停, 播放, 全屏等功能我们只能自己写代码解决
			这个时候我们可以使用插件方式来制作
	4.移动端常用开发框架:
		1.框架概述:
			框架, 顾名思义就是一套架构, 它会基于自身的特点向用户提供一套较为完整的解决方案. 框架的控制权在框架本身, 使用者要按照框架规定的某种规范进行开发.
			插件一般是为了解决某个问题而专门存在, 其功能单一, 并且比较小.
			前端常用的框架有 Bootstrap、 Vue、 Angular、 React 等. 既能开发 PC 端, 也能开发移动端
			前端常用的移动端插件有 swiper、 superslide、 iscroll 等.
			框架: 大而全, 一整套解决方案
			插件: 小而专一, 某个功能的解决方案
5.本地存储:
	1.本地存储特性:
		1.数据存储在用户浏览器中
		2.设置、 读取方便、 甚至页面刷新也不丢失数据
		3.容量较大, sessionStorage 约 5MB、 localStorage 约 20MB
		4.只能存储字符串, 可以将对象 JSON.stringify() 编码后存储
	2.window.sessionStorage:
		说明:
			1.生命周期为关闭浏览器窗口
			2.在同一个窗口下数据可以共享
			3.以键值对的形式存储使用
		使用:
			sessionStorage.setItem(key, value): 存储键值对
			sessionStorage.getItem(key): 根据键获取值
			sessionStorage.removeItem(key): 根据键删除数据
			sessionStorage.clear(): 清除所有的键值对
	3.window.localStorage:
		说明:
			1.生命周期为永久生效, 除非手动删除否则关闭页面也会存在
			2.在同一个浏览器下数据可以共享
			3.以键值对的形式存储使用
		使用:
			localStorage.setItem(key, value): 存储键值对
			localStorage.getItem(key): 根据键获取值
			localStorage.removeItem(key): 根据键删除数据
			localStorage.clear(): 清除所有的键值对
```
