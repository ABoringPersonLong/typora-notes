# 快捷键：

Ctrl + Shift + J：将选中的行合并成一行

Alt + 向左箭头：上一个编辑器

Alt + 向右箭头：下一个编辑器

Ctrl + B：定位至声明的位置

Ctrl + Alt + B：定位至选中类或者方法的具体实现

Ctrl + Shift + B:直接定位至光标所在变量的类型定义

Ctrl + U：直接定位至当前方法 override 或者 implements 的方法定义处

Ctrl + F12：显示当前文件的文件结构

Ctrl + Alt + F12：显示当前文件的路径，并可以方便的将相关父路径打开

Ctrl + H：显示当前类的继承层次

Ctrl + Shift + H：显示当前方法的继承层次

Ctrl + Alt + H：显示当前方法的调用层次

F2：定位至下一个错误处

Shift + F2：定位至前一个错误处

Ctrl + Alt + 向上箭头：查找前一个变量共现的地方

Ctrl + Alt + 向下箭头：查找下一个变量共现的地方

Ctrl + =：展开代码

Ctrl + -：收缩代码

Ctrl + Alt + =：递归展开代码

Ctrl + Alt + -：递归收缩代码

Ctrl + Shift + =：展开所有代码

Ctrl + Shift + -：收缩所有代码

Ctrl + Shitft + 向下箭头：将光标所在的代码块向下整体移动

Ctrl + Shift + 向上箭头：将光标所在的代码块向上整体移动

Ctrl + Alt + Shift + 向左箭头：将元素向左移动

Ctrl + Alt + Shift + 向右箭头：将元素向右移动

Alt + Shift + 向下箭头：将行向下移动

Alt + Shift + 向上箭头：将行向上移动

Ctrl + F：在当前文件中查找

Ctrl + R：替换字符串

Ctrl + Shift + F:在全局文件中查找字符串

Ctrl + Shift + R：在全局中替换字符串

Alt + F7：查找当前变量的使用，并列表显示

Ctrl + Alt + F7：查找当前变量的使用，并直接对话框提示

Ctrl + F7：在文件中查找符号的使用

Ctrl + Shift + F7：在文件中高亮显示变量的使用

Ctrl + O：重写基类方法

Ctrl + I：实现基类或接口中的方法

Alt + Insert：产生构造方法，get/set 方法等

Ctrl + Alt + T：将选中的代码使用 if、while、try/catch 等包装

Ctrl + Shitf + Delete：去除相关的包装代码

Alt + /：自动完成

Alt + Enter：自动提示完成，抛出异常

Ctrl + /：使用 // 注释

Ctrl + Shift + /：使用 /**/ 注释

Ctrl + Alt + L：格式化代码

Ctrl + Alt + O：优化 import

Ctrl + ]：快速跳转至诸如 {} 围起来的代码块的结尾处

Ctrl + [：快速跳转至诸如 {} 围起来的代码块的开头处

Ctrl + Shift + Enter：将输入的 if、for、函数等等补上 {} 或者，使代码语句完整

Shift + Enter：在当前行的下方开始新行

Ctrl + Alt + Enter：在当前行的上方插入新行

Ctrl + Shift + U：切换大小写

Shift + F6：重命名

Ctrl + Shift + F6：更改类型

# 设置：

## 1. 取消双击 Shift 打开全局搜索的快捷键：

1. 先找到 IDEA 安装目录下的 lib 目录下的 platform-impl.jar 文件，用压缩软件打开
2. 在压缩软件中找到 idea 文件夹下的 PlatformActions.xml 文件，把 com.intellij.ide.actions.SearchEverywhereAction 这一行注释掉

## 2. IDEA 部署 Tomcat 设置编码：

1. 修改 IDEA 文件 idea64.exe.vmoptions 里面末尾添加一行 -Dfile.encoding=UTF-8

2. 在 IDEA 中，打开 File -> Settings -> Editor -> File Encodings 在右侧窗口中将 3 个编码格式都改成 UTF-8

3. 打开 Tomcat 根目录下的 conf 目录，找到 web.xml 添加以下代码：

    ```xml
    <servlet>
        <servlet-name>default</servlet-name>
        <servlet-class>org.apache.catalina.servlets.DefaultServlet</servlet-class>
        <init-param>
            <param-name>debug</param-name>
            <param-value>0</param-value>
        </init-param>
        <!-- 添加这些代码 -->
        <init-param>
            <param-name>fileEncoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <!-- 添加这些代码 -->
        <init-param>
            <param-name>listings</param-name>
            <param-value>false</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    ```

4. 修改 server.xml 文件，添加以下代码：

    ```xml
    <!-- 修改前 -->
    <Connector connectionTimeout="20000" port="80" protocol="HTTP/1.1" redirectPort="8443"/>
    <!-- 修改后 -->
    <Connector connectionTimeout="20000" port="80" protocol="HTTP/1.1" redirectPort="8443" URIEncoding="UTF-8"/>
    ```

5. 打开 Tomcat 根目录下的 bin 目录，找到 catalina.bat 文件：

    在 set "JAVA_OPTS=%JAVA_OPTS% %JSSE_OPTS%" 这行代码下面添加 Dfile.encoding=UTF8 -Dsun.jnu.encoding=UTF8

6. 清除浏览器缓存即可