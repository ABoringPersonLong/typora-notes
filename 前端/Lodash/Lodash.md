# 1. 引入 Lodash

## 1. 通过 SDN 引入

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0">
  <!-- 引入 Lodash -->
  <script src="./lib/lodash.min.js"></script>
  <title>Title</title>
</head>
<body>
<script>
  // 使用 Lodash
  _.forEach({a: 1, b: 2}, (value, key) => console.log(value, key))
</script>
</body>
</html>
```

## 2. 通过 npm 安装

安装：

```sh
npm i lodash
```

使用：

```js
// 加载完整的构建
const _ = require('lodash')

// 使用 Lodash
_.forEach({a: 1, b: 2}, (value, key) => console.log(value, key))
```

# 2. 数组

## `_.intersection([arrays])`

创建唯一值的数组，这个数组包含所有给定数组都包含的元素，使用 [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero) 进行相等性比较。（注：可以理解为给定数组的交集）

```js
_.intersection([2, 1], [4, 2], [1, 2]) // [2]
```

## `_.union([arrays])`

创建一个按顺序排列的唯一值的数组。所有给定数组的元素值使用 [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero) 做等值比较。（注：`arrays`（数组）的并集，按顺序返回，返回数组的元素是唯一的）

```js
_.union([2], [1, 2]) // [2, 1]
```

## `_.uniq(array)`

创建一个去重后的 `array` 数组副本。使用了 [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero) 做等值比较。只有第一次出现的元素才会被保留。

```js
_.uniq([2, 1, 2]) // [2, 1]
```

## `_.uniqBy(array, [iteratee=_.identity])`

这个方法类似 [`_.uniq`](https://www.lodashjs.com/docs/lodash.uniqBy#uniq)，除了它接受一个 `iteratee` （迭代函数），调用每一个数组（`array`）的每个元素以产生唯一性计算的标准。iteratee 调用时会传入一个参数：**(value)**。

```js
_.uniqBy([2.1, 1.2, 2.3], Math.floor) // [2.1, 1.2]
_.uniqBy([{'x': 1}, {'x': 2}, {'x': 1}], item => item.x) // [{ 'x': 1 }, { 'x': 2 }]
_.uniqBy([{'x': 1}, {'x': 2}, {'x': 1}], 'x') // [{ 'x': 1 }, { 'x': 2 }]
```

## `_.xor([arrays])`

创建一个给定数组唯一值的数组，使用 [symmetric difference](https://en.wikipedia.org/wiki/Symmetric_difference) 做等值比较。返回值的顺序取决于他们数组的出现顺序。

```js
_.xor([2, 1], [2, 3]) // [1, 3]
```

## `_.zip([arrays])`

创建一个分组元素的数组，数组的第一个元素包含所有给定数组的第一个元素，数组的第二个元素包含所有给定数组的第二个元素，以此类推。

```js
_.zip(['fred', 'barney'], [30, 40], [true, false]) // [['fred', 30, true], ['barney', 40, false]]
```

# 3. 集合

## `_.forEach(collection, [iteratee=_.identity])`

调用 `iteratee` 遍历 `collection`(集合) 中的每个元素，iteratee 调用 3 个参数：*(value, index|key, collection)*。如果迭代函数（iteratee）显式的返回 `false` ，迭代会提前退出。

**注意**：与其他 “集合” 方法一样，类似于数组，对象的 “length” 属性也会被遍历。想避免这种情况，可以用 [`_.forIn`](https://www.lodashjs.com/docs/lodash.forEach#forIn) 或者 [`_.forOwn`](https://www.lodashjs.com/docs/lodash.forEach#forOwn) 代替。

```js
_([1, 2]).forEach(value => console.log(value)) // Logs `1` then `2`.
_.forEach({'a': 1, 'b': 2}, (value, key) => console.log(value, key)) // Logs '1 a' then '2 b' (iteration order is not guaranteed).
```

## `_.sample(collection)`

从 `collection`（集合）中获得一个随机元素。

```js
_.sample([1, 2, 3, 4]) // 2
```

## `_.shuffle(collection)`

创建一个被打乱值的集合。

```js
_.shuffle([1, 2, 3, 4]) // [4, 1, 3, 2]
```

# 4. 函数

## `_.debounce(func, [wait=0], [options=])`

创建一个 debounced（防抖动）函数，该函数会从上一次被调用后，延迟 `wait` 毫秒后调用 `func` 方法。 debounced（防抖动）函数提供一个 `cancel` 方法取消延迟的函数调用以及 `flush` 方法立即调用。 可以提供一个 options（选项） 对象决定如何调用 `func` 方法，`options.leading` 与|或 `options.trailing` 决定延迟前后如何触发（注：是 先调用后等待 还是 先等待后调用）。 `func` 调用时会传入最后一次提供给 debounced（防抖动）函数 的参数。 后续调用的 debounced（防抖动）函数返回是最后一次 `func` 调用的结果。

**注意**：如果 `leading` 和 `trailing` 选项为 `true`, 则 `func` 允许 trailing 方式调用的条件为: 在 `wait` 期间多次调用防抖方法。

如果 `wait` 为 `0` 并且 `leading` 为 `false`, `func` 调用将被推迟到下一个点，类似 `setTimeout` 为 `0` 的超时。

```js
// 避免窗口在变动时出现昂贵的计算开销。（150 毫秒内只有最后一次执行 calculateLayout() 函数会生效）
const calculateLayout = () => console.log('calculateLayout is running...')
window.addEventListener('resize', _.debounce(calculateLayout, 150))

// 当点击时 sendMail() 立即就被调用。
const sendMail = () => console.log('sendMail is running')
document.addEventListener('click', _.debounce(sendMail, 300, {
  leading: true, // 是否在延迟开始前调用
  trailing: false // 是否在延迟结束后调用
}))
```

## `_.throttle(func, [wait=0], [options=])`

创建一个节流函数，在 wait 秒内最多执行 `func` 一次的函数。 该函数提供一个 `cancel` 方法取消延迟的函数调用以及 `flush` 方法立即调用。 可以提供一个 options 对象决定如何调用 `func` 方法， options.leading 与|或 options.trailing 决定 wait 前后如何触发。 `func` 会传入最后一次传入的参数给这个函数。 随后调用的函数返回是最后一次 `func` 调用的结果。

**注意**：如果 `leading` 和 `trailing` 都设定为 `true` 则 `func` 允许 trailing 方式调用的条件为: 在 `wait` 期间多次调用。

如果 `wait` 为 `0` 并且 `leading` 为 `false`, `func`调用将被推迟到下一个点，类似`setTimeout`为`0`的超时。

```js
// 避免在滚动时过分的更新定位（每隔 100 毫秒才能执行一次 updatePosition() 函数）
const updatePosition = () => console.log('updatePosition is running...')
window.addEventListener('scroll', _.throttle(updatePosition, 100))
```

## `_.once(func)`

创建一个只能调用 `func` 一次的函数。重复调用返回第一次调用的结果。`func` 调用时，`this` 绑定到创建的函数，并传入对应参数。

```js
const initialize = _.once(() => console.log('createApplication'))
initialize() // createApplication
initialize() // 什么都没有，只能调用一次
```

# 5. 语言

## `_.isArray(value)`

检查 `value` 是否是 `Array` 类对象。

```js
_.isArray([1, 2, 3]) // true
_.isArray(document.body.children) // false
_.isArray('abc') // false
```

## `_.isDate(value)`

检查 `value` 是否是 `Date` 对象。

```js
_.isDate(new Date()) // true
_.isDate('Mon April 23 2012') // false
```

## `_.isElement(value)`

检查 `value` 是否是可能是 DOM 元素。

```js
_.isElement(document.body) // true
_.isElement('<body>') // false
```

## `_.isEmpty(value)`

检查 `value` 是否为一个空对象，集合，映射或者 set。判断的依据是除非是有枚举属性的对象，length 大于 0 的 arguments object, array, string 或类 jquery 选择器。

对象如果被认为为空，那么他们没有自己的可枚举属性的对象。

类数组值，比如 `arguments` 对象，array，buffer，string 或者类 jQuery 集合的 `length` 为 `0`，被认为是空。类似的，map（映射）和set 的 `size` 为 `0`，被认为是空。

```js
_.isEmpty(null) // true
_.isEmpty(true) // true
_.isEmpty(1) // true
_.isEmpty([1, 2, 3]) // false
_.isEmpty({'a': 1}) // false
```

## `_.isEqual(value, other)`

执行深比较来确定两者的值是否相等。

**注意**：这个方法支持比较 arrays, array buffers, booleans, date objects, error objects, maps, numbers, `Object` objects, regexes, sets, strings, symbols, 以及 typed arrays. `Object` 对象值比较自身的属性，不包括继承的和可枚举的属性。 **不支持函数和 DOM 节点比较**。

```js
const object = {'a': 1}
const other = {'a': 1}

_.isEqual(object, other) // true
object === other // false
```

# 6. 数学

## `_.max(array)`

计算 `array` 中的最大值。 如果 `array` 是 空的或者假值将会返回 `undefined`。

```js
_.max([4, 2, 8, 6]) // 8
_.max([]) // undefined
```

## `_.min(array)`

计算 `array` 中的最小值。 如果 `array` 是 空的或者假值将会返回 `undefined`。

```js
_.min([4, 2, 8, 6]) // 2
_.min([]) // undefined
```

## `_.sum(array)`

计算 `array` 中值的总和。

```js
_.sum([4, 2, 8, 6]) // 20
```

# 7. 字符串

## `_.truncate([string=''], [options=])`

截断 `string` 字符串，如果字符串超出了限定的最大值。 被截断的字符串后面会以 omission 代替，omission 默认是 "..."。

```js
_.truncate('hi-diddly-ho there, neighborino') // 'hi-diddly-ho there, neighbo...'

_.truncate('hi-diddly-ho there, neighborino', { // 'hi-diddly-ho there,...'
  length: 24, // 允许的最大长度，默认 30
  separator: ' ' // 截断点
})

_.truncate('hi-diddly-ho there, neighborino', { // 'hi-diddly-ho there...'
  length: 24,
  separator: /,? +/
})

_.truncate('hi-diddly-ho there, neighborino', { // 'hi-diddly-ho there, neig [...]'
  omission: ' [...]' // 超出后的代替字符，默认 ...
})
```

# 8. 实用函数

## `_.attempt(func, [args])`

尝试调用 `func`，返回结果或者捕捉错误对象。任何附加的参数都会在调用时传给 `func`。

**参数**

1. `func` *(Function)*: 要尝试调用的函数。
2. `[args]` *(...\*)*：调用 `func` 时，传递的参数。

**返回**

*(\*)*: 返回 `func` 结果或者错误对象。

```js
// 避免为无效的选择器抛出错误。
let elements = _.attempt(selector => document.querySelectorAll(selector), 'div') // 获取 div 元素
if (_.isError(elements)) elements = []
console.log(elements) // NodeList [div]

elements = _.attempt(selector => document.querySelectorAll(selector), '>_>') // 返回错误对象
if (_.isError(elements)) elements = []
console.log(elements) // []
```

## `_.range([start=0], end, [step=1])`

创建一个包含从 `start` 到 `end`，但不包含 `end` 本身范围数字的数组。如果 `start` 是负数，而 `end` 或 `step` 没有指定，那么 `step` 从 `-1` 为开始。如果 `end` 没有指定，`start` 设置为 `0`。如果 `end` 小于 `start`，会创建一个空数组，除非指定了 `step`。

**注意**：JavaScript 遵循 IEEE-754 标准处理无法预料的浮点数结果。

```js
_.range(4) // [0, 1, 2, 3]
_.range(-4) // [0, -1, -2, -3]
_.range(1, 5) // [1, 2, 3, 4]
_.range(0, 20, 5) // [0, 5, 10, 15]
_.range(0, -4, -1) // [0, -1, -2, -3]
_.range(1, 4, 0) // [1, 1, 1]
_.range(0) // []
```

