```
1.JavaScript简介：
  1.概念：
    一门客户端脚本语言
		运行在客户端浏览器中的。每一个浏览器都有JavaScript的解析引擎
		脚本语言：不需要编译，直接就可以被浏览器解析执行了
	2.功能：
		可以来增强用户和html页面的交互过程，可以来控制html元素，让页面有一些动态的效果，增强用户的体验
	3.JavaScript发展史：
		1.1992年，Nombase公司，开发出第一门客户端脚本语言，专门用于表单的校验。命名为：C--，后来更名为：ScriptEase。
		2.1995年，Netscape(网景)公司，开发了一门客户端脚本语言：LiveScript。后来，请来sun公司的专家，修改LiveScript，
      命名为JavaScript，Java跟JavaScript没有关系。
		3.1996年，微软抄袭JavaScript开发出JScript语言。
		4.1997年，ECMA(欧洲计算机制造商协会)，ECMAScript，就是所有客户端脚本语言的标准。
	4.浏览器执行 JavaScript 过程：
		浏览器分成两部分: 演染引擎和JS引擎
			渲染引擎: 用来解析 HTML 与 CSS, 俗称内核, 比如 chrome 浏览器的 blink, 老版本的 webkit
			JS 引擎: 也称为 JS 解释器. 用来读取网页中的 JavaScript 代码, 对其处理后运行, 比如 chrome 浏览器的 V8
		浏览器本身并不会执行 JS 代码, 而是通过内置 JavaScript 引擎(解释器)来执行 JS 代码. JS 引擎执行代码时逐行解释每一句源码(转换为机器语言),
		然后由计算机去执行, 所以 JavaScript 语言归为脚本语言, 会逐行解释执行.
	5.学习路线：
		JavaScript = ECMAScript + JavaScript自己特有的东西(BOM+DOM)
		先学 ECMAScript 再学 DOM 和 BOM，JavaScript 就学完了
2.JavaScript学习：
	1.ECMAScript：客户端脚本语言的标准
		1.基本语法：
			1.与html结合方式
        1.内部JS：
			    定义<script>标签，标签体内容就是js代码
			  2.外部JS：
			    定义<script>标签，通过src属性引入外部的js文件
			  注意：
          1.<script>可以定义在html页面的任何地方。但是定义的位置会音响执行顺序。
          2.<script>可以定义多个
			2.注释
        1.单行注释：//注释内容
        2.多行注释：/*注释内容*/
			3.数据类型
        1.原始数据类型(Java中的基本数据类型)：
          1.number：数字，整数/小数，NaN(not a number 一个不是数字的数字类型)
          2.string：字符串，"abc"或'abc'
          3.boolean：true或false
          4.null：一个对象为空的占位符
          5.undefined：未定义。如果一个变量没有给初始化值，则会被默认赋值为undefined
        2.引用数据类型：
          对象
				3.数据类型转换：
					1.转换为字符串类型：
						其他类型.toString(); -- 转换成字符串
						String(其他类型); -- 转换成字符串
						其他类型 + ""; -- 和字符串拼接的结果都是字符串
					2.转换为数字类型：
						parseInt("11"); -- 将 string 类型转成整数数字类型
						parseFloat("11.11"); -- 将 string 类型转成浮点数字类型
						Number("11"); -- 将 string 类型转成整数数字类型
						"11" - 0; -- 利用算术运算符隐式转换为数字类型，还可以用乘号或除号
					3.转换为布尔类型：
						Boolean(其他类型); -- 其他类型转成布尔类型
						代表空、否定的值会被转换为 false, 如: "", 0, NaN, null, undefined
						其余值都会被转换为 true
			4.变量
        1.变量：一小块存储数据的内存空间
			  2.Java语言是强类型语言，而JavaScript是弱类型语言。
			    强类型：在开辟变量存储空间时，定义了空间将来存储的数据的数据类型。只能存储固定类型的数据。
			    弱类型：在开辟变量存储空间时，不定义空间将来的存储数据类型，可以存放任意类型的数据。
			  3.语法：
			    var 变量名 = 初始化值;
			  4.typeof：获取变量的类型。
			  5.变量的定义的三中方法：
			    var: 变量，可以不赋初值
				  let: 块级作用域，在块级区域(如 if)中定于 let 变量，在区域外无影响
			    const: 常量，一经设置不可改变。在设置时必须赋初值
			5.运算符
        1.一元运算符：只有一个运算数的运算符
			    ++(自增)，--(自减)，+(正号)，-(负号)
			    ++，--：自增(自减)
			      ++(--) 在前，先自增(自减)，再运算
			      ++(--) 在后，先运算，在自增(自减)
			    +，-：正负号
			      代表一个数的正负
			      +123：正123
			      -123：负123
			    注意：在JS中，如果运算数不是运算符所要求的类型，那么js引擎会自动的将运算数进行类型转换
			      string转number：
			        按照string中的数转换，如果string中含有数字外的其他字符会转成NaN(不是数字的数字)
			      boolean转number：
			        true转成1，false转成0
			  2.算术运算符
			    + - * / % ...
          跟Java一样
        3.赋值运算符
			    = += -= ...
			    跟Java一样
			  4.比较运算符
			      > < >= <= == ===(全等于)
			    比较方式
			      1.类型相同：直接比较
			        字符串：按照字典顺序比较。按位逐一比较，直到得出大小为止。
			      2.类型不同：先进行类型转换，再比较
			        ===全等于。在比较之前，先判断类型，如果类型不一样，直接返回false
			  5.逻辑运算符
          && || !
          和Java一样
          在有条件的地方放入boolean型以外的类型会自动转成boolean型
          其他类型转boolean：
            1.number：0或NaN为假，其他为真
            2.string：除了空字符串("")，其他都是true
            3.null和undefined：都是false
            4.对象：都是true
        6.三元运算符
          ? :
          跟Java一样
			6.JS特殊语法
        1.语句以分号结尾，如果一行只有一条语句则分号可以省略(不建议)
          2.变量的定义使用var关键字，也可以不使用
            用：定义的变量是局部变量
            不用：定义的变量是全局变量(不建议)
			7.流程控制语句
			  1.if...else...
			    跟Java一样
			  2.switch
			    跟Java一样
			    在Java中，switch语句可以接受的数据类型：byte,int,short,char,枚举(1.5),String(1.7)
			      switch(变量):
			      case 值:
			    在JS中，switch语句可以接受任意的原始数据类型
			  3.while
			    跟Java一样
			  4.do...while
			    跟Java一样
			  5.for
			    跟Java一样
		2.基本对象
      Function：函数(方法)对象
		    1.创建：
		      1.
		        var fun = new Function(形参,方法体);
		      2.
		        function fun(形参) {
  		        方法体
	  	      }不用分号
		      3.
		        var 方法名 = function(形参) {
		          方法体
		        }不用分号
		    2.属性：
          1.length：形参的个数
		    3.特点：
          1.方法定义时，形参的类型不用写，返回值类型也不写
          2.方法定义是一个对象，后面定义的相同的方法会把前面的覆盖掉
          3.方法调用雨方法名称有关，与形参列表无关，形参可以随便传
          4.在方法声明中有一个隐藏的内置对象arguments(数组)，封装了所有的实际参数
		    4.调用：
          方法名(实参);
        5.方法：
          call 方法
            定义: 调用一个对象的一个方法，以另一个对象替换当前对象
            call 方法可以用来代替另一个对象调用一个方法
              在 js 的函数上可以使用 call 方法来改变函数中的 this 指向
              call 里面的第一个参数会改变调用 call 方法的函数内的 this
              不过第一个参数到达函数内部后会自动转成对象形式变成 this
              call 里面的第二个参数及之后则对应调用 call 方法的函数的第一个参数及之后
          call、apply、bind 三个方法的区别：
            共同点：都可以改变函数内部的 this 指向
            区别点：
              call 和 apply 传递的参数不一样，call 传递参数 aru1, aru2... 形式，apply 必须数组形式 [arg]
              bind 不会调用函数，可以改变函数内部 this 指向，永久改变
		  Array：数组对象
		    1.创建：
		      var array = new Array(元素列表);
          var array = new Array(长度);
          var array = [元素列表];
		    2.方法：
          join(参数)：将数组中的元素按照指定的分隔符拼接成字符串
          unshift(参数)：在第一条数据前面加一条新的数据
          push(参数)：向数组的尾部添加一个或多个元素，并返回数组的长度
          reverse()：反转并返回这个数组，会改变数组
          splice(5, 5[, 'aaa'])：从下标 5 开始往后截取 5 个元素，会改变原数组，如果有第三个参数，则；会把第三个参数插入到下标 5 的后面
          slice(5, 10[, 'aaa'])：截取下标 5 到位置 10 的元素，不会改变原数组，如果有第三个参数，则；会把第三个参数插入到下标 5 的后面
          pop()：删除数组中最后一个元素
          sort(回调函数)：方法以字母顺序对数组进行排序，如果是数字按第一个数来排序
            按数字大小进行排序：
              array.sort(function(a, b) {
                return a - b;
              });
          forEach(function (item, index, array) {})：遍历数组（中途不可停止循环）
            item: 必需。当前元素
            index: 可选。当前元素的索引值
            array: 可选。当前元素所属的数组对象
            例：
              array.forEach((item, index, array) => {
                console.log("元素: " + item);
                console.log("索引: " + index);
                console.log("当前正在遍历的数组: " + array);
              });
          some(function (item, index, array) {})：遍历数组（中途可停止循环）
            item: 必需。当前元素
            index: 可选。当前元素的索引值
            array: 可选。当前元素所属的数组对象
            例：
              array.some((item, index, array) => {
                console.log("元素: " + item);
                console.log("索引: " + index);
                console.log("当前正在遍历的数组: " + array);
              });
          every(function (item) {})：如果判断数组中的每一项都满足条件，就返回 true 反之 false
          filter(function (item, index, arr) {}): 过滤器，将满足条件的每一项放入一个新数组，再返回这个新数组
            第一个参数: item,必须,当前元素的值
            第二个参数 : index,可选,当前元素在数组中的索引值
            第三个参数 : arr,当前元素所处的数组对象
            filter方法特点：
              1.函数执行次数 === 数组长度
              2.函数内部的 return
                return true: 满足筛选条件，放入新数组中
                return false: 不满足条件，不放入新数组中
              3.filter方法的返回值
                返回筛选之后的新数组，如果没有符合条件的元素则返回空数组
              4.注意点:
                1.filter() 方法不会对空数组进行检测
                2.filter() 方法不会改变原始数组
          reduce(function (total, item) {}, 初始值): 累加
            total: 累加的结果
            item: 循环的每一项
            例：
            	将数组里的值全部加起来
            	const result = array.reduce((total, item) => total += item, 0)
          find(function (item, index, array) {})：返回数组中满足条件的一项，返回值：true 或 false
          findIndex(function (item, index) {})：返回数组中第一个满足条件的下标
		        3.属性：
		          length：数组的长度
		        4.特点：
		          1.数组的元素类型是可变的
		          2.数组的长度是可变的
		  Boolean：布尔对象
        1.创建：
          var flag = new Boolean(布尔值);
          var flag = Boolean(布尔值);
		  Date：日期对象
		    1.创建
		      var date = new Date();// 当前日期时间
          var date = new Date(2018, 11, 24, 10, 33, 30, 0);// 数字指定日期时间
            7 个数字分别指定年、月、日、小时、分钟、秒和毫秒(按此顺序)
            如果不足 7 个数，每少一个去掉最后一个，只有一个数时代表毫秒
          var date = new Date("2018-02-19 15:40:10");// 字符串指定日期时间
          var date = new Date(1642490683970);// 毫秒值指定日期时间
		    2.方法
		      获取：
            toLocaleString()：返回当前date对象应的时间本地字符串格式
            getFullYear()：获取年(yyyy)
            getMonth()：获取月(0-11)
            getDate()：获取天(1-31)
            getHours()：获取时(0-23)
            getMinutes()：获取分(0-59)
            getSeconds()：获取秒(0-59)
            getDay()：获取星期几(0-6)
            getTime()：获取毫秒值，从 1970 年 1 月 1 日 0 点至今的毫秒
            getMilliseconds()：获取最后 3 位毫秒(0-999)
          设置：
            setFullYear()：设置年(可选月和日)
            setMonth()：设置月(0-11)
            setDate()：设置日(1-31)
            setHours()：设置时(0-23)
            setMinutes()：设置分(0-59)
            setSeconds()：设置秒(0-59)
            setTime()：设置毫秒值
            setMilliseconds()：设置最后 3 位毫秒值(0-999)
		  Math：数学对象
		    1.创建：
		      对象不用创建直接使用。Math.方法名();
		    2.方法：
		      random()：返回0~1之间的随机数。包含0不包含1
		      round(数字)：返回最接近的整数。3.4为3  3.5为4
          ceil(数字)：返回最大整数。3.1为4
          floor(数字)：返回最小整数。3.9为3
          trunc(数字)：返回去掉小数的数字
					abs(任意类型值): 取绝对值, 不管是正的还是负的, 都返回正数, 如果是 null 返回 0
		    3.属性：
		      IP：返回圆周率
		  Number：数字对象
		    1.创建：
          var num = new Number(数字);
          var num = Number(数字);
		  String：字符对象
		    1.创建：
          var str = new String(字符串);
          var str = String(字符串);
        2.方法：
          toLowerCase(): 返回一个字符串，该字符串中的所有字母都被转换为小写字母
          toUpperCase(): 返回一个字符串，该字符串中的所有字母都被转换为大写字母
          includes()：是否包含指定的字符
          startsWith()：是否以指定的字符开头
          endsWith()：是否以指定的字符结尾
          str.substr(5, 5)：从下标 5 开始往后截取 5 个字符
          str.substring(5, 10)：从下标 5 开始截取到长度 10 之间的字符
		  RegExp：正则表达式对象
		    1.正则表达式：定义字符串的组成规则。
		      1.单个字符：[]
		        [a]：代表字母a
		        [ab]：代表字母a或b
		        [a-zA-Z]：代表任意一个字母
		        \d：代表单个数字字符[0-9]
		        \w：代表单个单词字符[a-zA-Z0-9_]
		      2.量词符号：
		        ?：表示出现0次或1次
		        *：表示出现0次或多次
		        +：表示出现1次或多次
		        {m}：表示刚好出现m次
		        {m,n}：表示出现的次数大于等于m小于等于n
		        {,n}：表示最多出现n次
		        {m,}：表示最少出现m次
		      3.开始结束符号
		        ^：开始，$：结束
		    2.正则对象：
		      1.创建
		        var reg = new RegExp("正则表达式");
		        var reg = /正则表达式/;
		      2.方法
		        test(字符串): 验证指定字符串是否符合指定正则规则
            exec(字符串): 方法的功能非常强大，它是一个通用的方法，而且使用起来也比 test() 方法以及支持正则表达式的 String 对象的方法更为复杂。
              如果 exec() 找到了匹配的文本，则返回一个结果数组。否则，返回 null。此数组的第 0 个元素是与正则表达式 (用括号括起来的) 匹配的文本，
              第 1 个元素是与 RegExpObject 的第 1 个子表达式相匹配的文本（如果有的话），第 2 个元素是与 RegExpObject 的第 2 个子表达式相匹配的文本（如果有的话），
              以此类推。除了数组元素和 length 属性之外，exec() 方法还返回两个属性。index 属性声明的是匹配文本的第一个字符的位置。input 属性则存放的是被检索的字符串 string。
              我们可以看得出，在调用非全局的 RegExp 对象的 exec() 方法时，返回的数组与调用方法 String.match() 返回的数组是相同的。
		  Global：全局对象
        1.特点：这个Global中封装的方法不需要对象就可以直接调用。
		    2.方法：
		      encodeURI(参数)：url编码
		      decodeURI(参数)：url解码
		      encodeURIComponent(参数)：url编码
		      decodeURIComponent(参数)：url解码
		      parseInt(参数)：将字符串转为数字
		        逐一判断每一个字符是否是数字，直到不是数字为止，将前边数字部分转为number
		      isNaN(参数)：判断一个值是否是NaN
		        NaN六亲不认，连自己都不认。NaN参与的==比较全部为false
		      eval(参数)：执行JavaScript字符串里的代码
		    3.URL编码
		      传智播客 = %E4%BC%A0%E6%99%BA%E6%92%AD%E5%AE%A2
		      假设编码是GBK，8个字节，每个字节8个二进制位：
		        1001 0101 1001 0101 1001 0101 1001 0101 1001 0101 1001 0101 1001 0101 1001 0101
		      每4个二进制位转换成一个十六进制数：
		        1001 0101
		        9    5
		      每两个十六进制数(就是一个字节)前面加个%
		        %95
		      最后组成 %E4%BC%A0%E6%99%BA%E6%92%AD%E5%AE%A2
		  自定义对象(json 对象)：
		    var user = {};// 创建空的 user 对象
		    var user = {username: "zhangsan", password: "123"};// 创建并赋值
		    user.username = "lisi";// 给属性赋值
		  使用构造函数：
			  function User(username, password) {// 定义构造函数
				  this.username = username;
					this.password = password;
			  }
				var user = new User("zhangsan", "123");// 创建并赋值
		  this 对象：
		    它拥有不同的值，具体取决于它的使用位置：
          在方法中，this 指的是所有者对象
          单独的情况下，this 指的是全局对象
          在函数中，this 指的是全局对象
          在函数中，严格模式下，this 是 undefined
          在事件中，this 指的是接收事件的元素
		3.预解析：
			1.js 引擎运行 js 分为两步: 预解析, 代码执行
				2.预解析 js 引擎会把 js 里面所有的 var 还有 function 提升到当前作用域的最前面
				3.代码执行, 按照代码书写的顺序从上往下执行
			2.预解析分为变量预解析(变量提升)和函数预解析(函数提升)
				1.变量提升: 就是把所有的变量声明提升到当前的作用域最前面, 不提升赋值操作
				2.函数提升: 就是把所有的函数声明提升到当前作用域的最前面, 不调用函数
```