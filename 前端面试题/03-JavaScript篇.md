# 一、数据类型

## 1. JavaScript 有哪些数据类型，它们的区别？

- 基本类型：number、string、boolean、null、undefined、(symbol、BigInt) 保存的是值。
  -  特点：
     1. 保存到栈区
     2. 基本类型值是不可变的（不能改变自身， 只能直接替换）
     3. 基本类型的比较是值比较
     4. 基本值的类型是不能添加属性和方法，添加了也获取不到
- 引用类型：（function、object、Array、Date、Mate、Set、Global 等）保存的是一个地址值。
  -  特点：
     1. 保存在堆中，地址值保存在栈区中，变量保存的是地址值
     2. 对象的值是可变的
     3. 变量和变量的比较是引用地址的比较，而不是对象值得比较

## 2. 数据类型检测的方式有哪些

1. typeof：可以检测的类型（基本类型）有：boolean undefined string number function
2. Object.prototype.toString.call(数据类型)：可以检测任意数据类型（推荐的）
3. instanceof：一般用于检测引用数据类型，通过 new 才会是实例。只能用来判断数组和对象，不能判断 string 和 boolean 类型，数组也属于对象
4. constructor：是 prototype 对象上的属性，指向构造函数，除了 null 和 undefined 报错，其他类型都可以使用
5. toString() 判断 string 和 boolean 类型
6. ===：有些类型只有一个值可以用全等判断：null undefined

## 3. 判断数组的方式有哪些

- 通过 Object.prototype.toString.call() 做判断

```javascript
Object.prototype.toString.call(obj).slice(8, -1) === 'Array';
```

- 通过原型链做判断

```javascript
obj.__proto__ === Array.prototype;
```

- 通过 ES6 的 Array.isArray() 做判断

```javascript
Array.isArrray(obj);
```

- 通过 instanceof 做判断

```javascript
obj instanceof Array
```

- 通过 Array.prototype.isPrototypeOf

```javascript
Array.prototype.isPrototypeOf(obj)
```

## 4. null 和 undefined 区别

首先 Undefined 和 Null 都是基本数据类型，这两个基本数据类型分别都只有一个值，就是 undefined 和 null。

undefined 代表的含义是**未定义**，null 代表的含义是**空对象**。一般变量声明了但还没有定义的时候会返回 undefined，null 主要用于赋值给一些可能会返回对象的变量，作为初始化。

当对这两种类型使用 typeof 进行判断时，null 类型会返回 “object”，这是一个历史遗留的问题。当使用双等号对两种类型的值进行比较时会返回 true，使用三个等号时会返回 false。

## 5. typeof null 的结果是什么，为什么？

typeof null 的结果是 Object。

在 JS 第一个版本中，所有值都存储在 32 位的单元中，每个单元包含一个小的 **类型标签(1-3 bits)** 以及当前要存储值的真实数据。而 null 的值是机器码 NULL 指针（null 指针的值全是 0），和 Object 的类型标签一样，所以会被判定为 Object。

## 6. intanceof 操作符的实现原理及实现

instanceof 运算符用于判断构造函数的 prototype 属性是否出现在对象的原型链中的任何位置。

```javascript
function myInstanceof(left, right) {
  // 获取对象的原型
  let proto = Object.getPrototypeOf(left)
  // 获取构造函数的 prototype 对象
  let prototype = right.prototype

  // 判断构造函数的 prototype 对象是否在对象的原型链上
  while (true) {
    if (!proto) return false
    if (proto === prototype) return true
    // 如果没有找到，就继续从其原型上找，Object.getPrototypeOf 方法用来获取指定对象的原型
    proto = Object.getPrototypeOf(proto)
  }
}
```

## 7. 为什么 0.1 + 0.2 !== 0.3，如何让其相等  

**第一种说辞**：

计算机是采用二进制方式存储数据的，0.1 的二进制是 0.000后面跟无限个1100，0.2 的二进制是：0.00后面跟无限个1100，这两个数的二进制都是无限循环的数，而 js 的 Number 类型的小数部分最多只能保留 52 位，再加上前面的 1，其实就是保留 53 位有效数字，剩余的需要舍去，遵从 “0舍1入” 的原则，所以，0.1 + 0.2 = 0.30000000000000004

**第二种说辞**：

因为在 0.1 + 0.2 进行计算的时候，实际上计算的是这两个数字在计算机里所存储的二进制，0.1 和 0.2 在进行二进制转换的时候会出现无限循环的情况

**第一种解决方案**：在开发过程中遇到类似这样的问题：

```javascript
let n1 = 0.1, n2 = 0.2
console.log(n1 + n2)  // 0.30000000000000004
```

这里得到的不是想要的结果，要想等于 0.3，就要把它进行转化：

```javascript
(n1 + n2).toFixed(2) // 注意，toFixed 为四舍五入
```

**第二种解决方案**：对于这个问题，一个直接的解决方法就是设置一个误差范围，通常称为 “机器精度”。对 JavaScript 来说，这个值通常为 2-52，在 ES6 中，提供了 `Number.EPSILON` 属性，而它的值就是 2-52，只要判断 `0.1 + 0.2 - 0.3` 是否小于 `Number.EPSILON`，如果小于，就可以判断为 0.1 + 0.2 === 0.3

## 8. isNaN 和 Number.isNaN 函数的区别？

- 函数 isNaN 接收参数后，会尝试将这个参数转换为数值，任何不能被转换为数值的的值都会返回 true，因此非数字值传入也会返回 true，会影响 NaN 的判断。
- 函数 Number.isNaN 会首先判断传入参数是否为数字，如果是数字再继续判断是否为 NaN，不会进行数据类型的转换，这种方法对于 NaN 的判断更为准确。

## 9. 其他值到字符串的转换规则？

- Null 和 Undefined 类型，null 转换为 "null"，undefined 转换为 "undefined"，
- Boolean 类型，true 转换为 "true"，false 转换为 "false"。
- Number 类型的值直接转换，不过那些极小和极大的数字会使用指数形式。
- Symbol 类型的值直接转换，但是只允许显式强制类型转换，使用隐式强制类型转换会产生错误。
- 对普通对象来说，除非自行定义 toString() 方法，否则会调用 toString()（Object.prototype.toString()）来返回内部属性 [[Class]] 的值，如 "[object Object]"。如果对象有自己的 toString() 方法，字符串化时就会调用该方法并使用其返回值。

## 10. 其他值到数字值的转换规则？

- Undefined 类型的值转换为 NaN。
- Null 类型的值转换为 0。
- Boolean 类型的值，true 转换为 1，false 转换为 0。
- String 类型的值转换如同使用 Number() 函数进行转换，如果包含非数字值则转换为 NaN，空字符串为 0。
- Symbol 类型的值不能转换为数字，会报错。
- 对象（包括数组）会首先被转换为相应的基本类型值，如果 valueOf() 和 toString() 均不返回基本类型值，会产生 TypeError 错误。

## 11. 其他值到布尔类型的值的转换规则？

以下这些是假值：undefined、null、false、NaN、""

假值的布尔强制类型转换结果为 false。从逻辑上说，假值列表以外的都应该是真值。

## 12. Object.is() 与比较操作符 `===`、`==` 的区别？

- 使用双等号（==）进行相等判断时，如果两边的类型不一致，则会进行强制类型转化后再进行比较。
- 使用三等号（===）进行相等判断时，如果两边的类型不一致时，不会做强制类型准换，直接返回 false。
- 使用 Object.is 来进行相等判断时，一般情况下和三等号的判断相同，它处理了一些特殊的情况，比如 -0 和 +0 不再相等，两个 NaN 是相等的。

## 13. JavaScript 中如何进行隐式类型转换？

用 `ToPrimitive` 方法，这是 JavaScript 中每个值隐含的自带的方法，用来将值（无论是基本类型值还是对象）转换为基本类型值。如果值为基本类型，则直接返回值本身；如果值为对象，其看起来大概是这样：

```javascript
/**
* @obj 需要转换的对象
* @type 期望的结果类型
*/
ToPrimitive(obj, type)
```

# 二、ES6

## 1. let、const、var 的区别

**（1）块级作用域：**块作用域由 `{}` 包括，let 和 const 具有块级作用域，var 不存在块级作用域。块级作用域解决了 ES5 中的两个问题。

**（2）变量提升：**var 存在变量提升，let 和 const 不存在变量提升，即在变量只能在声明之后使用，否在会报错。

**（3）给全局添加属性：**浏览器的全局对象是 window，Node 的全局对象是 global。var 声明的变量为全局变量，并且会将该变量添加为全局对象的属性，但是 let 和 const 不会。

**（4）重复声明：**var 声明变量时，可以重复声明变量，后声明的同名变量会覆盖之前声明的遍历。const 和 let 不允许重复声明变量。

**（5）暂时性死区：**在使用 let、const 命令声明变量之前，该变量都是不可用的。这在语法上，称为**暂时性死区**。使用 var 声明的变量不存在暂时性死区。

**（6）初始值设置：**在变量声明时，var 和 let 可以不用设置初始值。而 const 声明变量必须设置初始值。

**（7）指针指向：**let 和 const 都是 ES6 新增的用于创建变量的语法。let 创建的变量是可以更改指针指向（可以重新赋值）。但 const 声明的变量是不允许改变指针的指向。

## 2. const 对象的属性可以修改吗

const 保证的并不是变量的值不能改动，而是变量指向的那个内存地址不能改动。对于基本类型的数据（数值、字符串、布尔值），其值就保存在变量指向的那个内存地址，因此等同于常量。

但对于引用类型的数据（主要是对象和数组）来说，变量指向数据的内存地址，保存的只是一个指针，const 只能保证这个指针是固定不变的，至于它指向的数据结构是不是可变的，就完全不能控制了。

## 3. 如果 new 一个箭头函数的会怎么样

箭头函数是 ES6 中的提出来的，它没有 prototype，也没有自己的 this 指向，更不可以使用 arguments 参数，所以不能 new 一个箭头函数。

new 操作符的实现步骤如下：

1. 创建一个对象
2. 将构造函数的作用域赋给新对象（也就是将对象的 `__proto__` 属性指向构造函数的 prototype 属性）
3. 指向构造函数中的代码，构造函数中的 this 指向该对象（也就是为这个对象添加属性和方法）
4. 返回新的对象

所以，上面的第二、三步，箭头函数都是没有办法执行的。

## 4. 箭头函数与普通函数的区别

**（1）箭头函数比普通函数更加简洁**

**（2）箭头函数没有自己的 this**

**（3）箭头函数继承来的 this 指向永远不会改变**

**（4）call()、apply()、bind() 等方法不能改变箭头函数中 this 的指向**

**（5）箭头函数不能作为构造函数使用**

**（6）箭头函数没有自己的 arguments**

**（7）箭头函数没有 prototype**

## 5. 箭头函数的 this 指向哪⾥？

箭头函数不同于传统 JavaScript 中的函数，箭头函数并没有属于⾃⼰的 this，它所谓的 this 是捕获其所在上下⽂的 this 值，作为⾃⼰的 this 值，并且由于没有属于⾃⼰的 this，所以是不会被 new 调⽤的，这个所谓的 this 也不会被改变。

## 6. 对 rest 参数的理解

扩展运算符被用在函数形参上时，**它还可以把一个分离的参数序列整合成一个数组**：

```javascript
function mutiple(...args) {
  console.log(args)
}
mutiple(1, 2, 3, 4) // [1, 2, 3, 4]
```

## 7. ES6 中模板语法与字符串处理

- 在模板字符串中，空格、缩进、换行都会被保留
- 允许用 ${} 的方式嵌入变量。并且支持 “运算” 式的表达式

# 三、JavaScript 基础

## 1. new 操作符的实现原理

**new 操作符的执行过程**：

（1）首先创建了一个新的空对象

（2）设置原型，将对象的原型设置为函数的 prototype 对象

（3）让函数的 this 指向这个对象，执行构造函数的代码（为这个新对象添加属性）

（4）判断函数的返回值类型，如果是值类型，返回创建的对象。如果是引用类型，就返回这个引用类型的对象

## 2. map 和 Object 的区别

|          | Map                                                          | Object                                                       |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 意外的键 | Map 默认情况不包含任何键，只包含显式插入的键。               | Object 有一个原型, 原型链上的键名有可能和自己在对象上的设置的键名产生冲突。 |
| 键的类型 | Map 的键可以是任意值，包括函数、对象或任意基本类型。         | Object 的键必须是 String 或是 Symbol。                       |
| 键的顺序 | Map 中的 key 是有序的。因此，当迭代的时候，Map 对象以插入的顺序返回键值。 | Object 的键是无序的。                                        |
| Size     | Map 的键值对个数可以轻易地通过 size 属性获取。               | Object 的键值对个数只能手动计算。                            |
| 迭代     | Map 是 iterable 的，所以可以直接被迭代。                     | 迭代 Object 需要以某种方式获取它的键然后才能迭代。           |
| 性能     | 在频繁增删键值对的场景下表现更好。                           | 在频繁添加和删除键值对的场景下未作出优化。                   |

## 3. JavaScript 脚本延迟加载的方式有哪些？

延迟加载就是等页面加载完成之后再加载 JavaScript 文件。js 延迟加载有助于提高页面加载速度。

一般有以下几种方式：

- **defer 属性：**给 js 脚本添加 defer 属性，这个属性会让脚本的加载与文档的解析同步解析，然后在文档解析完成后再执行这个脚本文件，这样的话就能使页面的渲染不被阻塞。多个设置了 defer 属性的脚本按规范来说最后是顺序执行的，但是在一些浏览器中可能不是这样。
- **async 属性：**给 js 脚本添加 async 属性，这个属性会使脚本异步加载，不会阻塞页面的解析过程，但是当脚本加载完成后立即执行 js 脚本，这个时候如果文档没有解析完成的话同样会阻塞。多个 async 属性的脚本的执行顺序是不可预测的，一般不会按照代码的顺序依次执行。
- **动态创建 DOM 方式：**动态创建 DOM 标签的方式，可以对文档的加载事件进行监听，当文档加载完成后再动态的创建 script 标签来引入 js 脚本。
- **使用 setTimeout 延迟方法：**设置一个定时器来延迟加载 js 脚本文件。
- **让 JS 最后加载：**将 js 脚本放在文档的底部，来使 js 脚本尽可能的在最后来加载执行。

## 4. JavaScript 类数组对象的定义？

javascript 定义类数组对象的方法是：1、首先创建一个空对象；2、为对象直接定义数字下标的属性；3、关键点，为对象设置 length 属性和 splice 属性为数字和函数。

js 中类数组对象很多，概念简单的讲就是看上去像数组，又不是数组，可以使用数字下标方式访问又没有数组方法。

## 5. 数组有哪些原生方法？

- 数组和字符串的转换方法：toString()、toLocalString()、join() 其中 join() 方法可以指定转换为字符串时的分隔符。
- 数组尾部操作的方法 pop() 和 push()，push 方法可以传入多个参数。
- 数组首部操作的方法 shift() 和 unshift() 重排序的方法 reverse() 和 sort()，sort() 方法可以传入一个函数来进行比较，传入前后两个值，如果返回值为正数，则交换两个参数的位置。
- 数组连接的方法 concat()，返回的是拼接好的数组，不影响原数组。
- 数组截取办法 slice()，用于截取数组中的一部分返回，不影响原数组。
- 数组插入方法 splice()，影响原数组查找特定项的索引的方法，indexOf() 和 lastIndexOf() 迭代方法 every()、some()、filter()、map() 和 forEach() 方法。
- 数组归并方法 reduce() 和 reduceRight() 方法。

## 6. 为什么函数的 arguments 参数是类数组而不是数组？如何遍历类数组？

`arguments` 是一个对象，它的属性是从 0 开始依次递增的数字，还有 `callee` 和 `length` 等属性，与数组相似；但是它却没有数组常见的方法属性，如 `forEach`、`reduce` 等，所以叫它们类数组。

要遍历类数组，有三个方法：

（1）将数组的方法应用到类数组上，这时候就可以使用 `call` 和 `apply` 方法，如：

```javascript
function foo(){ 
  Array.prototype.forEach.call(arguments, a => console.log(a))
}
```

（2）使用 Array.from 方法将类数组转化成数组：‌

```javascript
function foo(){ 
  const arrArgs = Array.from(arguments)
  arrArgs.forEach(a => console.log(a))
}
```

（3）使用展开运算符将类数组转化成数组：

```javascript
function foo(){
    const arrArgs = [...arguments]
    arrArgs.forEach(a => console.log(a))
}
```

## 7. 什么是 DOM 和 BOM？

- DOM 指的是文档对象模型，它指的是把文档当做一个对象，这个对象主要定义了处理网页内容的方法和接口。
- BOM 指的是浏览器对象模型，它指的是把浏览器当做一个对象来对待，这个对象主要定义了与浏览器进行交互的方法和接口。BOM 的核心是 window，而 window 对象具有双重角色，它既是通过 js 访问浏览器窗口的一个接口，又是一个 Global（全局）对象。这意味着在网页中定义的任何对象，变量和函数，都作为全局对象的一个属性或者方法存在。window 对象含有 location 对象、navigator 对象、screen 对象等子对象，并且 DOM 的最根本的对象 document 对象也是 BOM 的 window 对象的子对象。

## 8. 对类数组对象的理解，如何转化为数组

一个拥有 length 属性和若干索引属性的对象就可以被称为类数组对象，类数组对象和数组类似，但是不能调用数组的方法。常见的类数组对象有 arguments 和 DOM 方法的返回结果，函数参数也可以被看作是类数组对象，因为它含有 length 属性值，代表可接收的参数个数。

常见的类数组转换为数组的方法有这样几种：

- 通过 call 调用数组的 slice 方法来实现转换

```javascript
Array.prototype.slice.call(arrayLike);
```

- 通过 call 调用数组的 splice 方法来实现转换

```javascript
Array.prototype.splice.call(arrayLike, 0);
```

- 通过 apply 调用数组的 concat 方法来实现转换

```javascript
Array.prototype.concat.apply([], arrayLike);
```

- 通过 Array.from 方法来实现转换

```javascript
Array.from(arrayLike);
```

## 9. 对 AJAX 的理解，实现一个 AJAX 请求

AJAX 是 Asynchronous JavaScript and XML 的缩写，指的是通过 JavaScript 的异步通信，从服务器获取 XML 文档从中提取数据，再更新当前网页的对应部分，而不用刷新整个网页。

创建 AJAX 请求的步骤：

- **创建一个 XMLHttpRequest 对象。**
- 在这个对象上**使用 open 方法创建一个 HTTP 请求**，open 方法所需要的参数是请求的方法、请求的地址、是否异步和用户的认证信息。
- 当对象的属性和监听函数设置完成后，最后调**用 send 方法来向服务器发起请求**，可以传入参数作为发送的数据体。
- 在发起请求前，可以为这个对象**添加一些信息和监听函数**。比如说可以通过 setRequestHeader 方法来为请求添加头信息。还可以为这个对象添加一个状态监听函数。一个 XMLHttpRequest 对象一共有 5 个状态，当它的状态变化时会触发 onreadystatechange 事件，可以通过设置监听函数，来处理请求成功后的结果。当对象的 readyState 变为 4 的时候，代表服务器返回的数据接收完成，这个时候可以通过判断请求的状态，如果状态是 2xx 或者 304 的话则代表返回正常。这个时候就可以通过 response 中的数据来对页面进行更新了。

## 10. JavaScript 为什么要进行变量提升，它导致了什么问题？

主要有以下两个原因：

- 提高性能
- 容错性更好

导致了的问题：由于遍历时定义的 i 会变量提升成为一个全局变量，在函数结束之后不会被销毁，所以打印出来 11。

## 11. ES6 模块与 CommonJS 模块有什么异同？

ES6 Module 和 CommonJS 模块的区别：

- CommonJS 是对模块的浅拷⻉，ES6 Module 是对模块的引⽤，即 ES6 Module 只存只读，不能改变其值，也就是指针指向不能变，类似 const；
- import 的接⼝是 read-only（只读状态），不能修改其变量值。即不能修改其变量的指针指向，但可以改变变量内部指针指向，可以对 commonJS 重新赋值（改变指针指向），但是对 ES6 Module 赋值会编译报错。

ES6 Module 和 CommonJS 模块的共同点：

- CommonJS 和 ES6 Module 都可以对引⼊的对象进⾏赋值，即对对象内部属性的值进⾏改变。

## 12. 如何判断一个对象是否属于某个类？

- 第一种方式，使用 instanceof 运算符来判断构造函数的 prototype 属性是否出现在对象的原型链中的任何位置。
- 第二种方式，通过对象的 constructor 属性来判断，对象的 constructor 属性指向该对象的构造函数，但是这种方式不是很安全，因为 constructor 属性可以被改写。
- 第三种方式，如果需要判断的是某个内置的引用类型的话，可以使用 Object.prototype.toString() 方法来打印对象的[[Class]] 属性来进行判断。

## 13. for...in 和 for...of 的区别

for...of 是 ES6 新增的遍历方式，允许遍历一个含有 iterator 接口的数据结构（数组、对象等）并且返回各项的值，和 ES3 中的 for...in 的区别如下

- for...of 遍历获取的是对象的键值，for...in 获取的是对象的键名；
- for...in 会遍历对象的整个原型链，性能非常差不推荐使用，而 for...of 只遍历当前对象不会遍历原型链；
- 对于数组的遍历，for...in 会返回数组中所有可枚举的属性（包括原型链上可枚举的属性），for...of 只返回数组的下标对应的属性值；

**总结：**for...in 循环主要是为了遍历对象而生，不适用于遍历数组；for...of 循环可以用来遍历数组、类数组对象，字符串、Set、Map 以及 Generator 对象。

## 14. 数组的遍历方法有哪些

| **方法**                  | **是否改变原数组** | **特点**                                                     |
| ------------------------- | ------------------ | ------------------------------------------------------------ |
| forEach()                 | 否                 | 数组方法，不改变原数组，没有返回值                           |
| map()                     | 否                 | 数组方法，不改变原数组，有返回值，可链式调用                 |
| filter()                  | 否                 | 数组方法，过滤数组，返回包含符合条件的元素的数组，可链式调用 |
| for...of                  | 否                 | for...of 遍历具有 Iterator 迭代器的对象的属性，返回的是数组的元素、对象的属性值，不能遍历普通的obj对象，将异步循环变成同步循环 |
| every() 和 some()         | 否                 | 数组方法，some() 只要有一个是 true，便返回 true；而 every() 只要有一个是 false，便返回 false |
| find() 和 findIndex()     | 否                 | 数组方法，find() 返回的是第一个符合条件的值；findIndex() 返回的是第一个返回条件的值的索引值 |
| reduce() 和 reduceRight() | 否                 | 数组方法，reduce() 对数组正序操作；reduceRight() 对数组逆序操作 |

## 15. forEach 和 map 方法有什么区别

这方法都是用来遍历数组的，两者区别如下：

- forEach() 方法会针对每一个元素执行提供的函数，对数据的操作会改变原数组，该方法没有返回值；
- map() 方法不会改变原数组的值，返回一个新数组，新数组中的值为原数组调用函数处理之后的值；

# 四、原型与原型链

## 1. 对原型、原型链的理解

**原型**：在 JavaScript 中是使用构造函数来新建一个对象的，每一个构造函数的内部都有一个 prototype 属性，它的属性值是一个对象，这个对象包含了可以由该构造函数的所有实例共享的属性和方法。当使用构造函数新建一个对象后，在这个对象的内部将包含一个指针，这个指针指向构造函数的 prototype 属性对应的值，在 ES5 中这个指针被称为对象的原型。一般来说不应该能够获取到这个值的，但是现在浏览器中都实现了 `__proto__` 属性来访问这个属性，但是最好不要使用这个属性，因为它不是规范中规定的。ES5 中新增了一个 Object.getPrototypeOf() 方法，可以通过这个方法来获取对象的原型。

**原型链**：当访问一个对象的属性时，如果这个对象内部不存在这个属性，那么它就会去它的原型对象里找这个属性，这个原型对象又会有自己的原型，于是就这样一直找下去，也就是原型链的概念。原型链的尽头一般来说都是 Object.prototype 所以这就是新建的对象为什么能够使用 toString() 等方法的原因。

**特点**：JavaScript 对象是通过引用来传递的，创建的每个新对象实体中并没有一份属于自己的原型副本。当修改原型时，与之相关的对象也会继承这一改变。

## 2. 原型修改、重写

```javascript
function Person(name) {
    this.name = name
}
// 修改原型
Person.prototype.getName = function() {}
var p = new Person('hello')
console.log(p.__proto__ === Person.prototype) // true
console.log(p.__proto__ === p.constructor.prototype) // true
// 重写原型
Person.prototype = {
    getName: function() {}
}
var p = new Person('hello')
console.log(p.__proto__ === Person.prototype) // true
console.log(p.__proto__ === p.constructor.prototype) // false
```

可以看到修改原型的时候 p 的构造函数不是指向 Person 了，因为直接给 Person 的原型对象直接用对象赋值时，它的构造函数指向的了根构造函数 Object，所以这时候 `p.constructor === Object`，而不是 `p.constructor === Person`。要想成立，就要用 constructor 指回来：

```javascript
Person.prototype = {
    getName: function() {}
}
var p = new Person('hello')
p.constructor = Person
console.log(p.__proto__ === Person.prototype) // true
console.log(p.__proto__ === p.constructor.prototype) // true
```

## 3. 原型链指向

```javascript
p.__proto__ // Person.prototype
Person.prototype.__proto__ // Object.prototype
p.__proto__.__proto__ // Object.prototype
p.__proto__.constructor.prototype.__proto__ // Object.prototype
Person.prototype.constructor.prototype.__proto__ // Object.prototype
p1.__proto__.constructor // Person
Person.prototype.constructor // Person
```

# 五、执行上下文/作用域链/闭包

## 1. 对闭包的理解

**闭包是指有权访问另一个函数作用域中变量的函数**，创建闭包的最常见的方式就是在一个函数内创建另一个函数，创建的函数可以访问到当前函数的局部变量。

闭包有两个常用的用途；

- 闭包的第一个用途是使我们在函数外部能够访问到函数内部的变量。通过使用闭包，可以通过在外部调用闭包函数，从而在外部访问到函数内部的变量，可以使用这种方法来创建私有变量。
- 闭包的另一个用途是使已经运行结束的函数上下文中的变量对象继续留在内存中，因为闭包函数保留了这个变量对象的引用，所以这个变量对象不会被回收。

比如，函数 A 内部有一个函数 B，函数 B 可以访问到函数 A 中的变量，那么函数 B 就是闭包。

## 2. 对作用域、作用域链的理解

作用域是一个空间，在一个作用域中不能访问另一个作用域，作用域是分层的，内层作用域可以访问外层作用域，反之不行。

**（1）全局作用域**

- 最外层函数和变量拥有全局作用域
- 所有未定义直接赋值的变量自动声明为全局作用域
- 所有 window 对象的属性拥有全局作用域
- 全局作用域有很大的弊端，过多的全局作用域变量会污染全局命名空间，容易引起命名冲突

**（2）函数作用域**

- 声明在函数内部的变量就是函数作用域，一般只有固定的代码片段可以访问到

**（3）块级作用域**

- 使用 ES6 中新增的 let 和 const 指令可以声明块级作用域，块级作用域可以在函数中创建也可以在一个代码块中的创建（由 `{}` 包裹的代码片段）
- let 和 const 声明的变量不会有变量提升，也不可以重复声明
- 在循环中比较适合绑定块级作用域，这样就可以把声明的计数器变量限制在循环内部

**（4）作用域链**

在当前作用域中查找所需变量，但是该作用域没有这个变量，那这个变量就是自由变量。如果在自己作用域找不到该变量就去父级作用域查找，依次向上级作用域查找，直到访问到 window 对象就被终止，这一层层的关系就是作用域链。

## 3. 对执行上下文的理解

**（1）全局执行上下文**

任何不在函数内部的都是全局执行上下文，它首先会创建一个全局的 window 对象，并且设置 this 的值等于这个全局对象，一个程序中只有一个全局执行上下文。

**（2）函数执行上下文**

当一个函数被调用时，就会为该函数创建一个新的执行上下文，函数的上下文可以有任意多个。

# 六、this/call/apply/bind

## 1. 对 this 对象的理解

this 是执行上下文中的一个属性，它指向最后一次调用这个方法的对象。在实际开发中，this 的指向可以通过四种调用模式来判断。

- 第一种是**构造器调用模式**，如果一个函数用 new 调用时，函数执行前会新创建一个对象，this 指向这个新创建的对象。
- 第二种是 **apply、call 和 bind 调用模式**，这三个方法都可以指定调用函数的 this 指向。但是这个函数的 this 指向除了使用 new 时会被改变，其他情况下都不会改变。
- 第三种是**方法调用模式**，如果一个函数作为一个对象的方法来调用时，this 指向这个对象。
- 第四种是**函数调用模式**，当一个函数不是一个对象的属性时，直接作为函数来调用时，this 指向全局对象。

这四种方式，使用构造器调用模式的优先级最高，然后是 apply、call 和 bind 调用模式，然后是方法调用模式，然后是函数调用模式。

## 2. call() 和 apply() 的区别？

它们的作用一模一样，区别仅在于传入参数的形式的不同。

- call 传入的参数数量不固定，跟 apply 相同的是，第一个参数也是代表函数体内的 this 指向，从第二个参数开始往后，每个参数被依次传入函数。
- apply 接受两个参数，第一个参数指定了函数体内 this 对象的指向，第二个参数为一个带下标的集合，这个集合可以为数组，也可以为类数组，apply 方法把这个集合中的元素作为参数传递给被调用的函数。

# 七、异步编程

## 1. 异步编程的实现方式？

JavaScript 中的异步机制可以分为以下几种：

- **回调函数** 的方式，使用回调函数的方式有一个缺点是，多个回调函数嵌套的时候会造成回调函数地狱，上下两层的回调函数间的代码耦合度太高，不利于代码的可维护。
- **Promise** 的方式，使用 Promise 的方式可以将嵌套的回调函数作为链式调用。但是使用这种方法，有时会造成多个 then 的链式调用，可能会造成代码的语义不够明确。
- **generator** 的方式，它可以在函数的执行过程中，将函数的执行权转移出去，在函数外部还可以将执行权转移回来。当遇到异步函数执行的时候，将函数执行权转移出去，当异步函数执行完毕时再将执行权给转移回来。因此在 generator 内部对于异步操作的方式，可以以同步的顺序来书写。使用这种方式需要考虑的问题是何时将函数的控制权转移回来，因此需要有一个自动执行 generator 的机制，比如说 co 模块等方式来实现 generator 的自动执行。
- **async 函数** 的方式，async 函数是 generator 和 promise 实现的一个自动执行的语法糖，它内部自带执行器，当函数内部执行到一个 await 语句的时候，如果语句返回一个 promise 对象，那么函数将会等待 promise 对象的状态变为 resolve 后再继续向下执行。因此可以将异步逻辑，转化为同步的顺序来书写，并且这个函数可以自动执行。

## 2. setTimeout、Promise、Async/Await 的区别

1. setTimeout 的回调函数放到宏任务队列里，等到执行栈清空以后执行
2. Promise 构造函数是同步执行的，then 方法是异步执行的
3. async/await 搭配 Promise，可以通过编写形似同步的代码来处理异步流程

## 3. 对 Promise 的理解

Promise 是异步编程的一种解决方案，它是一个对象，可以获取异步操作的消息，改善了异步编程的困境，避免了地狱回调，它比传统的解决方案回调函数和事件更合理和更强大。

Promise 是一个构造函数，接收一个函数作为参数，返回一个 Promise 实例，Promise 的实例有**三个状态**：

- Pending（进行中）
- Resolved（已完成）
- Rejected（已拒绝）

**Promise 的特点**：

- 对象的状态不受外界影响。
- 一旦状态改变就不会再变。

**Promise 的缺点**：

- 无法取消 Promise，一旦新建它就会立即执行，无法中途取消。
- 如果不设置回调函数，Promise 内部抛出的错误，不会反应到外部。
- 当处于 pending 状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

**注意**：在构造 `Promise` 的时候，构造函数内部的代码是立即执行的

## 4. Promise 的基本用法

**（1）创建 Promise 对象**：

Promise 对象代表一个异步操作，有三种状态：pending（进行中）、fulfilled（已成功）和 rejected（已失败）。

Promise 构造函数接受一个函数作为参数，该函数的两个参数分别是 `resolve` 和 `reject`。

```javascript
const promise = new Promise(function(resolve, reject) {
  // ... some code
  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

一般情况下都会使用 `new Promise()` 来创建 promise 对象，但是也可以使用 `promise.resolve` 和 `promise.reject` 这两个方法

**（2）Promise 方法**：

- then()：接受两个回调函数作为参数。第一个回调函数是 Promise 对象的状态变为 `resolved` 时调用，第二个回调函数是 Promise 对象的状态变为 `rejected` 时调用
- catch()：捕获异常
- all()：发起并行的 Promise 异步操作，等**所有的异步操作全部结束后**才会执行下一步的 .then 操作（等待机制）
- race()：发起并行的 Promise 异步操作，**只要任何一个异步操作完成，就立即执行下一步的 .then 操作**（赛跑机制）
- finally()：不管 Promise 对象最后状态如何，都会执行的操作

## 5. Promise 解决了什么问题

解决了回调地狱的问题，用 .then 链式调用

## 6. Promise.all 和 Promise.race 的区别的使用场景

**（1）Promise.all**

`Promise.all` 可以将多个 `Promise` 实例包装成一个新的 Promise 实例。同时，成功和失败的返回值是不同的，成功的时候返回的是**一个结果数组**，而失败的时候则返回**最先被 reject 失败状态的值**。

Promise.all 中传入的是数组，返回的也是数组，并且会将进行映射，传入的 promise 对象返回的值是按照顺序在数组中排列的，但是注意的是他们执行的顺序并不是按照顺序的，除非可迭代对象为空。

**（2）Promise.race**

顾名思义，Promse.race 就是赛跑的意思，意思就是说，Promise.race([p1, p2, p3]) 里面哪个结果获得的快，就返回那个结果，不管结果本身是成功状态还是失败状态。当要做一件事，超过多长时间就不做了，可以用 `timeOutPromise` 方法来解决：

```javascript
Promise.race([promise1, timeOutPromise(5000)]).then(res => {})
```

## 7. 对 async/await 的理解

async/await 其实是 `Generator` 的语法糖，它能实现的效果都能用 then 链来实现，它是为优化 then 链而开发出来的。从字面上来看，async 是 “异步” 的简写，await 则为等待，所以很好理解 async 用于申明一个 function 是异步的，而 await 用于等待一个异步方法执行完成。当然语法上强制规定 await 只能出现在 asnyc 函数中。

async 函数返回的是一个 Promise 对象。async 函数会返回一个 Promise 对象，如果在函数中 `return` 一个直接量，async 会把这个直接量通过 `Promise.resolve()` 封装成 Promise 对象。

那如果 async 函数没有返回值，又该如何？很容易想到，它会返回 `Promise.resolve(undefined)`。

## 8. await 到底在等啥？

await 表达式的运算结果取决于它等的是什么。

- 如果它等到的不是一个 Promise 对象，那 await 表达式的运算结果就是它等到的东西。
- 如果它等到的是一个 Promise 对象，await 就忙起来了，它会阻塞后面的代码，等着 Promise 对象 resolve，然后得到 resolve 的值，作为 await 表达式的运算结果。

## 9. async/await 的优势

如果需要处理由多个 Promise 组成的 then 链的时候，可以 async/await 进一步优化 Promise 的 .then，让代码读起来更加同步。

## 10. async/await 对比 Promise 的优势

- 进一步优化 Promise 的 .then，让代码读起来更加同步
- Promise 传递中间值⾮常麻烦，⽽ async/await ⼏乎是同步的写法，⾮常优雅
- 错误处理友好，async/await 可以⽤成熟的 try/catch，而 Promise 的错误捕获⾮常冗余
- 调试友好，Promise 的调试很差，由于没有代码块，你不能在⼀个返回表达式的箭头函数中设置断点，如果你在⼀个 .then 代码块中使⽤调试器的步进（step-over）功能，调试器并不会进⼊后续的 .then 代码块，因为调试器只能跟踪同步代码的每⼀步。

# 八、面向对象

## 1. 对象创建的方式有哪些？

- 字面量的形式直接创建对象
- 构造函数模式
- 原型模式
- 工厂模式
- 组合使用构造函数模式和原型模式
- 动态原型模式
- 寄生构造函数模式

## 2. 对象继承的方式有哪些？

- 原型链的方式来实现继承
- 借用构造函数的方式继承
- 组合继承
- 原型式继承
- 寄生式继承
- 寄生式组合继承

# 九、垃圾回收与内存泄漏

## 1. 浏览器的垃圾回收机制

**（1）垃圾回收的概念**

**垃圾回收**：JavaScript 代码运行时，需要分配内存空间来储存变量和值。当变量不在参与运行时，就需要系统收回被占用的内存空间，这就是垃圾回收。

**（2）减少垃圾回收**

- **对数组进行优化：**在清空一个数组时，最简单的方法就是给其赋值为 []，但是与此同时会创建一个新的空对象，可以将数组的长度设置为 0，以此来达到清空数组的目的。
- **对** `object` **进行优化：**对象尽量复用，对于不再使用的对象，就将其设置为 null，尽快被回收。
- **对函数进行优化：**在循环中的函数表达式，如果可以复用，尽量放在函数的外面。

## 2. 哪些情况会导致内存泄漏

- **意外的全局变量：**由于使用未声明的变量，而意外的创建了一个全局变量，而使这个变量一直留在内存中无法被回收。
- **被遗忘的计时器或回调函数：**设置了 setInterval 定时器，而忘记取消它，如果循环函数有对外部变量的引用的话，那么这个变量会被一直留在内存中，而无法被回收。
- **脱离 DOM 的引用：**获取一个 DOM 元素的引用，而后面这个元素被删除，由于一直保留了对这个元素的引用，所以它也无法被回收。
- **闭包：**不合理的使用闭包，从而导致某些变量一直被留在内存当中。