# 1. 引入 Moment.js

## 1. 通过 SDN 引入

```html
<script src="./lib/moment.min.js"></script>
```

## 2. 通过 npm 安装

安装：

```sh
npm i moment
```

引入：

```js
const moment = require('moment')

moment().format()
```

# 2. 多语言支持

```js
moment.locale('zh-cn') // 设置语言为 zh-cn（中文），默认为 en（英文）
```

# 3. 日期格式化

```js
moment().format('MMMM Do YYYY, h:mm:ss a') // 九月 5日 2022, 10:18:00 上午（月 日 年, 时:分:秒 上午/下午）
moment().format('dddd') // 星期一（星期几）
moment().format('MMM Do YY') // 9月 5日 22（月 日 年的后两位）
moment().format('YYYY [escaped] YYYY') // 2022 escaped 2022（年 escaped 年）
moment().format() // 2022-09-05T10:18:00+08:00（年-月-日T时:分:秒+上午/下午）
```

# 4. 相对时间

```js
moment('2011-10-31', 'YYYY-MM-DD').fromNow() // 11 年前（2011 年 10 月 31 距离现在的时间）
moment('2012-06-20', 'YYYY-MM-DD').fromNow() // 10 年前（2012 年 06 月 20 距离现在的时间）
moment().startOf('day').fromNow() // 11 小时前（一天前距离现在的时间）
moment().endOf('day').fromNow() // 13 小时内（一天前在现在的时间以内）
moment().startOf('hour').fromNow() // 31 分钟前（上一个小时距离现在的时间）
```

# 5. 日历时间

```js
moment().subtract(10, 'days').calendar() // 2022/08/26（10 天前）
moment().subtract(6, 'days').calendar() // 上周二10:42（6 天前）
moment().subtract(3, 'days').calendar() // 上周五10:42（3 天前）
moment().subtract(1, 'days').calendar() // 昨天10:31（1 天前）
moment().calendar() // 今天10:31
moment().add(1, 'days').calendar() // 明天10:31（1 天后）
moment().add(3, 'days').calendar() // 本周四10:42（3 天后）
moment().add(10, 'days').calendar() // 2022/09/15（10 天后）
```