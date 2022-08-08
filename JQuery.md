```
JQuery 基础：
    1.概念：一个 JavaScript 端架。简化 JS 开发
        jQuery 是一个快速、简洁的JavaScript框架，是继Prototype之后又一个优秀的JavaScript代码库(框架)于2006年1月由John Resig发布。
        jQuery 设计的宗旨是“write Less，Do More”，即写更少的代码，做更多的事情。
        它封装 JavaScript 常用的功能代码，提供一种简便的 JavaScript 设计模式，优化 HTML 文档操作、事件处理、动画设计和 Ajax 交互。
        JavaScript 框架：本质上就是一些 JS 文件，封装了 JS 的原生代码而已
    2.快速入门：
        1.步骤：
            1.下载 JQuery：
                目前 jQuery 有三个大版本：
                    1.x：兼容 ie678，使用最为广泛的，官方只做 BUG 维护，
                        功能不再新增。因此一般项目来说，使用 1.x 版本就可以了，
                        最终版本：1.12.4 (2016 年 5 月 20 日)
                    2.x：不兼容 ie678，很少有人使用，官方只做 BUG 维护，
                        功能不再新增。如果不考虑兼容低版本的浏览器可以使用 2.x，
                        最终版本：2.2.4 (2016 年 5 月 20 日)
                    3.x：不兼容 ie678，只支持最新的浏览器。除非特殊要求，
                        一般不会使用 3.x 版本的，很多老的 jQuery 插件不支持这个版本。
                        目前该版本是官方主要更新维护的版本。
                jquery-xx.js 与 jquery-xxx.min.js 区别：
                    1.jquery-xxx.js：开发版本。给程序员看的，有良好的缩进和注释
                    2.jquery-xxx.min.js：生产版本。程序中使用，没有缩进。体积小一些。程序加载更快
            2.导入 JQuery 的 js 文件：
                导入 min.js 文件
            3.使用：
                var div1 = $("#div1");// 根据 id 获取元素对象
                alert(div1.html());// 输出 div1 的标签体内容
    3.JQuery 对象和 JS 对象的区别与转换：
        1.JQuery 对象在操作是，更加方便。
        2.JQuery 对象和 JS 对象方法不通用
        3.两者相互转换：
            jq -> js：jq 对象[索引] 或 jq 对象.get(索引)
            js -> jq；$(JS 对象)
    4.选择器：筛选具有相似特征的元素(标签)
        1.基本语法学习：
            1.事件绑定：
                相当于：document.getElementById("button").onclick = function () {}
                去掉最前面的 on
                $("#button").click(function () {
                    alert("按钮被点击了...");
                });
            2.入口函数：
                DOM 文档加载完成之后执行该函数中的代码。相当于：window.onload = function () {}
                $(function () {
                });
                window.onload 和 $(function) 的区别：
                    window.onload 只能定义一次，如果定义多次，后面的会将前面的覆盖掉
                    $(function) 可以定义多次
            3.样式控制：
                $("#div1").css("background-color", "red"); 第一种
                $("#div1").css("backgroundColor", "red"); 第二种，这种写法按住 Ctrl 键把鼠标放上去可以检查是否写对
        2.分类：
            1.基本选择器：
                1.标签选择器(元素选择器)：
                    语法：$("html 标签名") 获取所有匹配标签名的元素
                2.id 选择器：
                    语法：$("#id 的属性值") 获取与指定 id 属性值匹配的元素
                3.类选择器：
                    语法：$(".class 的属性值") 获取与指定的 class 属性值匹配的元素
                4.并集选择器：
                    语法：$("元素1,元素2...") 选择所有 A 和 B 元素
            2.层级选择器：
                1.后代选择器：
                    语法：$("A B") 选择 A 元素内部的所有 B 元素
                2.子选择器：
                    语法：$("A > B") 选择 A 元素内部的所有 B 子元素
            3.属性选择器：
                1.属性名称选择器：
                    语法：$("A[属性名]") 选择包含指定属性名的元素
                2.属性选择器：
                    语法：$("A[属性名='值']") 选择包含指定属性名等于指定值的元素
                    语法：$("A[属性名!='值']") 选择包含指定属性名不等于指定值的元素
                    语法：$("A[属性名^='te']") 选择包含指定属性名的值以 te 开头的元素
                    语法：$("A[属性名$='te']") 选择包含指定属性名的值以 st 结尾的元素
                    语法：$("A[属性名*='te']") 选择包含指定属性名的值包含 es 的元素
                3.复合属性选择器：
                    语法：$("A[属性名1='值1'][属性名2='值2']...") 选择包含多个属性条件的元素
            4.过滤选择器：
                1.首元素选择器：
                    语法：:first 获取选择的元素中的第一个元素
                2.尾元素选择器：
                    语法：:last 获取选择的元素中最后一个元素
                3.非元素选择器：
                    语法：:not(selector) 不包含指定内容的元素
                4.偶数选择器：
                    语法：:even 偶数，从 0 开始计数
                5.奇数选择器：
                    语法：:odd 奇数，从 0 开始计数
                6.等于索引选择器：
                    语法：:eq(index) 指定索引元素
                7.大于索引选择器：
                    语法：:gt(index) 大于指定索引元素
                8.小于索引选择器：
                    语法：:lt(index) 小于指定索引元素
                9.标题选择器：
                    语法：:header 获取标题元素，固定写法
            5.表单过滤选择器：
                1.可用元素选择器：
                    语法：:enabled 获取可用元素
                2.不可用元素选择器：
                    语法：:disabled 获取不可用元素
                3.单选/复选框选中选择器：
                    语法：:checked 获取单选/复选框选中的元素
                4.下拉框选中选择器：
                    语法：:selected 获取下拉框选中的元素
    5.DOM 操作：
        1.内容操作：
            html()：获取/设置元素的标签体内容
                <div>111</div> 这样，获取的是 111
                <div><span>111</span></div> 如果是这样，获取的是 <span>111</span>
            text()：获取/设置元素的标签体纯文本内容
                <div>111</div> 这样，获取的是 111
                <div><span>111</span></div> 如果是这样，获取的还是 111
            val()：获取/设置元素的 value 属性值
        2.属性操作：
            1.通用属性操作：
                attr()：获取/设置元素的属性值
                removeAttr()：删除属性
                prop()：获取/设置元素的属性值
                removeProp()：删除属性
                attr 和 prop 区别？
                    如果操作的是元素的自定义属性，则建议使用 attr
                    如果操作的是元素的固有属性，则建议使用 prop
            2.对 class 属性操作：
                addClass()：添加 class 属性值
                removeClass()：删除 class 属性值
                toggleClass()：切换 class 属性
                    例如：toggleClass("one");
                        判断如果元素对象上存在 class="one"，则将属性值 one 删除掉
                        如果元素对象上不存在 class="one"，则添加
            3.设置样式：
                $(window).height()：获取高度
        3.CRUD 操作：
            append()：父元素将一个子元素追加到末尾
                对象1.addend(对象2)：将对象2添加到对象1元素内部，并且在末尾
            prepend()：父元素将一个子元素追加到开头
                对象1.prepend(对象2)：将对象2添加到对象1元素内部，并且在开头
            appendTo()：跟 append() 相反
                对象1.appendTo(对象2)：将对象1添加到对象2元素内部，并且在末尾
            prepend()：跟 prepend() 相反
                对象1.prepend(对象2)：将对象1添加到对象2元素内部，并且在开头
            after()：添加元素到元素后面
                对象1.after(对象2)：将对象2添加到对象1后面，对象1和对象2是兄弟关系
            before()：添加元素到元素前面
                对象1.before(对象2)：将对象2添加到对象1前面，对象1和对象2是兄弟关系
            insertAfter()：跟 after() 相反
                对象1.insertAfter(对象2)：将对象1添加到对象2后面，对象1和对象2是兄弟关系
            insertBefore()：跟 before() 相反
                对象1.insertBefore(对象2)：将对象1添加到对象2前面，对象1和对象2是兄弟关系
            remove()：移除元素
                对象.remove()：将此对象删除掉
            empty()：清空元素的所有后代元素
                对象.empty()：将对象的后代元素全部清空，但是保留当前对象以及其属性节点
            clone()：复制元素
                对象.clone()：复制一个新的对象出来
            next()：获取元素的下一个兄弟元素
            nextAll()：获取元素后面所有的兄弟元素
            prev()：获取元素的上一个兄弟元素
            prevAll()：获取元素前面所有的兄弟元素
            siblings()：获取元素的所有兄弟元素
            children()：获取元素的所有子元素
            find()：获取元素的所有子元素和后代元素
            parent()：获取元素的父元素
JQuery 高级：
    1.动画：
        1.默认显示和隐藏方式：
            show(speed, easing, fn)：显示
            hide(speed, easing, fn)：隐藏
            toggle(speed, easing, fn)：切换
        2.滑动显示和隐藏方式：
            slideDown(speed, easing, fn)：显示
            slideUp(speed, easing, fn)：隐藏
            slideToggle(speed, easing, fn)：切换
        3.淡入淡出显示和隐藏方式：
            fadeIn(speed, easing, fn)：显示
            fadeOut(speed, easing, fn)：隐藏
            fadeToggle(speed, easing, fn)：切换
        4.自定义动画：
            animate(params, [speed], [easing], [fn]);
            params: 想要更改的样式属性，以对象形式传递，必须写。属性名可以不用带引号，如果是复合属性则需要采取驼峰命名法 borderLeft。其余参数都可以省略。
        5.以上三种方式的参数：
            1.speed：动画的速度。三个预定义的值("slow", "normal", "fast")越后面的越快，可以自定义毫秒值
            2.easing：用来指定切换效果，默认是"swing"，可用参数"linear"
                swing：动画执行时效果是先慢，中间块，最后又慢
                linear：动画执行时速度是匀速的
            3.fn：在动画完成时执行的函数，每个元素执行一次
    2.遍历：
        1.js 的遍历方式：
            for (初始化值; 循环结束条件; 步长)
        2.jq 的遍历方式：
            1.jq对象.each(callback)
                lis.each(function (index, element) {
                    document.write($(this).html());
                    document.write(index+":"+$(element).html());
                });
            2.$.each(object, [callback])
                $.each(lis, function (index, element) {
                    document.write($(this).html());
                    document.write(index+":"+$(element).html());
                });
            3.for...of：JQuery3.0 版本之后提供的方式
                for (var li of lis) {
                    document.write($(li).html());
                }
    3.事件绑定：
        1.jquery 标准的绑定方式：
            jq对象.事件方法(回调函数)：绑定事件
        2.on 绑定事件/off 解除绑定
            jq对象.on("事件名称", 回调函数)：绑定事件
            jq对象.off("事件名称")：解除事件
        3.事件切换：toggle
            jq对象.toggle(fn1, fn2...)：点一下执行 fn1，再点一下执行 nf2...
            注意：1.9 版本之后 .toggle() 方法删除，需要导入 jquery-migrate (迁移)插件可以恢复此功能
        4.事件名称就是 js 的事件名去掉最前面的 on
    4.插件：
        1.实现方式：
            1.$.fn.extend(object)
                增强通过 JQuery 获取的对象的功能，如：通过 $("#id") 获取的
            2.$.extend(object)
                增强 JQuery 对象自身的功能，如：$ 或 jQuery 点出来的
    5.jQuery 尺寸：
        width() / height(): 获取匹配元素宽度和高度值, 只算 width / height
        innerWidth() / innerHeight(): 获取匹配元素宽度和高度值, 包含 padding
        outerWidth() / outerHeight(): 获取匹配元素宽度和高度值, 包含 padding、border
        outerWidth(true) / outerHeight(true): 获取匹配元素宽度和高度值, 包含 padding、border、margin
    6.jQuery 位置：
        位置主要有三个: offset()、 position()、 scrollTop()/scrollLeft()
```

