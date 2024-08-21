```
HTML
    1.概念
        HTML(Hyper Text Markup Language)：超文本标记语言
            超文本：
                超文本是用超链接的方法，将各种不用空间的文字信息组织在一起的网状文本。
            标记语言：
                由标签构成的语言。<标签名称> 如 html，xml
                标记语言不是编程语言
    2.快速入门：
        语法：
            1.html文档后缀名 .html 或 .htm
            2.标签分为：
                1.围堵标签：有开始标签和结束标签。如 <html> </html>
                2.自闭和标签：开始标签和结束标签在一起。如 <br/>
            3.标签可以嵌套：
                需要正确嵌套，不能你中有我，我中有你
                错误：<html><head></html></head>
                正确：<html><head></head></html>
            4.在开始标签中可以定义属性。属性是由键值对构成，值需要用引号(单双都可以)引起来
            5.html的标签不区分大小写，但是建议使用小写。
    3.标签学习：
        1.文件标签：构成html最基本的标签
            <!DOCTYPE html>：html5中定义该文档是html文档
            html：html文档的跟标签
                lang="ch"：中国
            <meta charset="UTF-8">：设置编码
            head：头标签。用于指定html文档的一些属性。引入外部的资源
            title：标题标签
            body：体标签
        2.文本标签：和文本有关的标签
            &nbsp; 空格
            &gt; 大于号
            &lt; 小于号
            &quot; 引号
            &copy; 版权符号
            <h1>~<h6>：标题标签
            <p>：段落标签
            <br>：换行标签
            <hr>：展示一条水平线
            <b>：字体加粗
            <i>：字体斜体
            <u>：下划线
            <s>：删除线
            <font>：字体标签
            <center>：文本居中
            属性定义：
                color：
                    1.可以写颜色的单词，如：red,green,blue
                    2.rgb(值1,值2，值3)：值的范围：0~255 如：rgb(255,0,0)
                    3.#值1值2值3：值的范围：00~FF之间，如：#FF00FF
                width：
                    1.数值：width="20"，20像素
                    2.数值%：width="20%"，占屏幕的百分之20
            <pre>：保留文本格式
            <code>：代码
            <acronym>：首字母缩写
            <address>：地址
            <blockquote>：长引用
            <q>：短引用
        3.图片标签：
            <img src="./a.jpg" alt="图片加载失败" width="200" height="100">
            ./代表当前目录 ../代表上一级目录
            抽取公共路径：
                <!-- 抽取公共路径 -->
                <base href="./images/">
                <!-- 会在路径前面自动拼接上公共路径 -->
                <img src="a.jpg" alt="图片加载失败" width="200">
        4.列表标签：
            有序列表：
                <ol>
                    <li>张</li>
                    <li>李</li>
                </ol>
            无序列表：
                <ul>
                    type：disc实体圆(默认) square实体方块 circle空心圆
                    <li>张</li>
                    <li>李</li>
                </ul>
            定义列表：
                <dl>
                    <dt>左</dt>
                    <dd>右</dd>
                </dl>
        5.链接标签：
            <a href="https://www.baidu.com">跳转至百度</a>
            <a href="https://www.baidu.com" target="_blank">跳转至百度打开一个新窗口</a>
        6.div和span
            div：每一个div占满一整行，块级标签
            span：文本信息在一行展示，行内标签，内联标签
        7.语义化标签：
            html5中为了提高可读性，提供的一些标签
            <header>：页眉
            <footer>：页脚
        8.表格标签：
            <table>：定义表格
                border：边框
                bordercolor：边框颜色
                bgcolor：背景色
                width：表格宽度
                height：表格高度
                align：水平对齐方式，值：
                    left左，center中，right右
                valign：垂直对齐方式，值：
                    top顶，middle中，bottom低，baseline基线
                cellpadding：内容与边框的距离
                cellspacing：单元格与表格之间的距离
            <tr>：定义行
                bgcolor：背景色
                align：水平对齐方式
            <td>：定义单元格
                bgcolor：背景色
                align：水平对齐方式
                rowspan：合并行
                colspan：合并列
            <th>：定义表头单元格
            <caption>：表格标题
            <thead>：表头
            <tbody>：表体
            <tfoot>：表尾
        9.表单标签：
            <form>：用于定义表单。可以定义一个范围，范围代表采集用户数据的范围
                action：指定提交数据的URL
                method：指定提交方式，一共7中，2种比较常用
                    get：
                        1.请求参数会在地址栏中显示。会封装到请求行中。
                        2.请求参数的长度是有限制的。
                        3.不太安全，因为参数会显示出来。
                    post：
                        1.请求参数不会在地址栏中显示。会封装在请求体中。
                        2.请求参数的长度没有限制。
                        3.较为安全，因为参数不会显示出来。
                表单项中的数据要想被提交，必须指定其name属性
            表单项标签：
                <input>：通过type属性，改变元素展示的样式
                    type值：
                        text：输入框(默认)
                        password：密码输入框
                        radio：单选框
                        checkbox：复选框
                        file：文件选择框
                        submit：提交按钮
                        reset：重置按钮
                        button：普通按钮
                        image：图片按钮
                        color：取色器
                        date：年月日
                        datetime-local：年月日时分
                        email：邮箱输入框
                        number：数字输入框
                        url：网址
                        range：滑块
                        search：搜索框
                        hidden：隐藏域
                    		placeholder：提示文字
											checked：默认选择
                    		readonly：只读
		                    disabled：禁用
    		                required：必填
        		            pattern：验证规则，值是正则表达式
            		        autocomplete="off"：不显示历史输入记录
											size：长度，对于text和password以字符为单位，其他以像素为单位
                <label>：与input中的id关联后，点击被label包裹的内容也会进入input标签
                <select>：下拉列表(单选)，加个 multiple="multiple" 属性就变成多选的下拉列表
                <option>
						selected：默认选择
                <textarea>：文本域
                    cols列数(宽度)，rows行数(高度)
				<fieldset>：域，一个框框
					<legend>：域标题，可以不写
        10.窗口标签：
            将 index.html 文件的内容导入到一个小窗口来
            <iframe src="index.html" id="iframeId"></iframe>
            window.parent.document.getElementById("#iframeId");// 在窗口里面获取外面的 iframe 元素
        11.音频标签：
            <audio>：用于播放音频
                src：音频文件的路径
                controls：显示播放的控件
                autoplay：自动播放（部分浏览器不支持）
                loop：循环播放
        12.视频标签：
            <audio>：用于播放视频
                src：视频文件的路径
                controls：显示播放的控件
                autoplay：自动播放（谷歌浏览器中必须静音才能播放）
                muted：静音
                loop：循环播放
```