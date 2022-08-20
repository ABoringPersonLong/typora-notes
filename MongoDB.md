# 1. 安装 MongoDB

## 1. 安装 MongoDB Community Server

网址：https://www.mongodb.com/try/download/community

偶数版本为稳定版，奇数版本为开发版

选择自定义安装（custom），安装到 E:\MongoDB\Server\6.0\bin 目录

## 2. 配置环境变量

E:\MongoDB\Server\6.0\bin

## 3. 启动 mongodb 服务器

安装时默认已经启动了后台 mongodb 服务，对应配置文件是 E:\MongoDB\Server\6.0\bin\mongod.cfg

也可以手动启动：打开 cmd 窗口，输入 mongod --dbpath E:\MongoDB\Server\6.0\data

## 4. 安装 MongoDB Shell 连接 mongodb

网址：https://www.mongodb.com/try/download/shell

直接下载压缩包解压到 E:\MongoDB 文件夹下即可

将解压出来的 bin 目录添加到环境变量：E:\MongoDB\mongosh-1.5.4-win32-x64\bin

在 cmd 中输入 mongosh 即可进入命令行界面

> **在 MongoDB5 之前**，安装好以后**直接输入 mongo 即可进入命令行界面**。
>
> MongoDB5 应该直接把 Shell 集成在 MongoDB 中了，所以下载好可以直接使用。
>
> **但是 MongoDB6 必须单独安装 Shell**

# 2. 基本概念

1. 数据库（database）
2. 集合（collection）
3. 文档（document）
   - 在 MongoDB 中，数据库和集合都不需要手动创建，当我们创建文档时，如果文档所在的集合或数据库不存在，会自动创建数据库和集合

# 3. 指令

## 1. 基本指令

1. show databases 或 show dbs
   - 显示所有数据库
2. use 数据库名
   - 进入到指定的数据库中
3. db
   - db 表示的是当前所处的数据库
4. db.dropDatabase()
   - 删除当前数据库
5. show collections
   - 显示当前数据库中的所有集合
6. db.集合名.drop()
   - 删除当前数据库下的指定集合

## 2. 插入指令

1. db.集合名.insert(文档)
   - 向集合中插入一个文档（该指令已弃用，会报警告）
2. db.集合名.insert([文档1, 文档2, ...])
   - 向集合中插入多个文档（该指令已弃用，会报警告）
3. db.集合名.insertOne(文档)
   - 向集合中插入一个文档
4. db.集合名.insertMany([文档1, 文档2, ...])
   - 向集合中插入多个文档

## 3. 查询指令

1. db.集合名.find()
   - 查询集合里面的所有文档
2. db.集合名.find({})
   - 查询集合里面的所有文档
3. db.集合名.find().count()
   - 查询集合里面的文档总数
4. db.集合名.find({_id: '1'})
   - 查询集合里面 _id 为 1 的所有文档
5. db.集合名.find({name: 'zhangsan', age: 18})
   - 查询集合里面 name 为 zhangsan 且 age 为 18 的所有文档
6. db.集合名.findOne({name: 'zhangsan'})
   - 只查询一个文档
7. db.集合名.findOne({name: 'zhangsan'}).age
   - 只查询一个文档，且只显示 age 字段
8. db.集合名.find().sort({num: 1})
   - 按照 num 升序显示
9. db.集合名.find().sort({num: -1})
   - 按照 num 降序显示
10. db.集合名.find({name: 'zhangsan'}, {_id: 0, name: 1, age: 1})
    - 不显示 \_id，显示 name 和 age（\_id 默认是 1，其他字段默认是 0）

## 4. 修改指令

1. db.集合名.update({name: 'zhangsan'}, {$set: {age: 30}})
   - 将 name 为 zhangsan 的文档的 age 改为 30，只会改变一个（该指令已弃用，会报警告）
   - $set 表示设置属性
   - $unset 表示删除属性
2. db.集合名.update({}, {}, {upsert: true, multi: true})
   - upsert：表示如果不存在要修改的文档，是否插入新文档，true 为插入，默认是 false 不插入
   - multi：默认是 false，只更新找到的第一条记录，如果这个参数为 true，就把按条件查出来多条记录全部更新
3. db.集合名.updateOne({name: 'zhangsan'}, {$set: {age: 40}})
   - 将 name 为 zhangsan 的文档的 age 改为 40，只会改变一个
   - $set 表示设置属性
   - $unset 表示删除属性
4. db.集合名.updateMany({name: 'zhangsan'}, {$set: {age: 40}})
   - 将 name 为 zhangsan 的文档的 age 改为 40，会改变多个
   - $set 表示设置属性
   - $unset 表示删除属性

## 5. 删除指令

1. db.students.remove({})
   - 删除全部（该指令已弃用，会报警告）
2. db.集合名.remove({name: 'zhangsan'})
   - 删除 name 为 zhangsan 的文档，全部删除（该指令已弃用，会报警告）
3. db.students.remove({name: 'zhangsan'}, true)
   - 删除 name 为 zhangsan 的文档，删除一个（该指令已弃用，会报警告）
4. db.students.deleteOne({name: 'zhangsan'})
   - 删除 name 为 zhangsan 的文档，删除一个
5. db.students.deleteMany({})
   - 删除全部
6. db.students.deleteMany({name: 'zhangsan'})
   - 删除 name 为 zhangsan 的文档，删除全部

# 4. 练习题

## 1. 向 students 中插入 100 条数据

```js
const array = []
for (let i = 1; i <= 100; i++) {
  array.push({num: i + ''})
}
db.students.insertMany(array)
```

## 2. 查询 students 中 num 大于 50 的文档

```js
db.students.find({num: {$gt: 50}})
```

## 3. 查询 students 中 num 小于 50 的文档

```js
db.students.find({num: {$lt: 50}})
```

## 4. 查询 students 中 num 大于 40 小于 50 的文档

```js
db.students.find({num: {$gt: 40, $lt: 50}})
```

## 5. 查询 students 中前 10 条数据

```js
db.students.find().limit(10) // limit：显示几条数据
```

## 6. 查询 students 中第 11 到第 20 条数据

```js
db.students.find().limit(10).skip(10) // skip：跳过几条数据
```

## 7. 查询 students 中 num 小于 10 或大于 90 的数据

```js
db.students.find({
  $or: [
    {num: {$lt: 10}},
    {num: {$gt: 90}}
  ]
})
```

# 5. mongoose

## 1. 快速使用

1. 安装：

   ```bash
   npm i mongoose
   ```

2. 引入 mongoose

   ```js
   const mongoose = require('mongoose')
   ```

3. 连接 MongoDB 数据库

   ```js
   mongoose.connect('mongodb://localhost:27017/test') // test 是数据库名
   ```

4. 监听 MongoDB 数据库连接状态

   ```js
   // 数据库连接成功的事件
   mongoose.connection.once('open', () => console.log('数据库连接成功'))
   
   // 数据库连接断开的事件
   mongoose.connection.once('close', () => console.log('数据库连接断开'))
   ```

5. 断开连接

   ```js
   mongoose.disconnect()
   ```

## 2. mongoose 的三个核心对象

### 1. Schema

```js
const mongoose = require('mongoose')

const {Schema} = mongoose

// 创建 Schema 对象
const studentSchema = new Schema({
  name: String, // String 是 {type: String} 的简写
  age: Number,
  gender: {
    default: '男',
    type: String
  }
})
```

### 2. Model

```js
// 创建 Model 对象
const StudentModel = mongoose.model('students', studentSchema) // 第一个参数是数据库里的集合名称

// ************************************************ 插入数据 ************************************************
// 插入一个文档
StudentModel.create({
  name: 'zhangsan',
  age: 18,
  gender: '男'
}).then(result => console.log('01 == ', result), error => console.log('01 == ', error))

// 插入多个文档
StudentModel.create([
  {
    name: 'zhangsan',
    age: 20,
    gender: '男'
  },
  {
    name: 'lisi',
    age: 20,
    gender: '女'
  }
]).then(result => console.log('02 == ', result), error => console.log('02 == ', error))

// ************************************************ 查询数据 ************************************************
// 查询全部文档，也可以传一个空对象 {}
StudentModel.find().then(result => console.log('03 == ', result))

// 查询所有名为 zhangsan 且年龄大于等于 18 的文档
StudentModel.find({name: 'zhangsan', age: {$gte: 18}}).then(result => console.log('04 == ', result))

// 将结果传递给回调
StudentModel.find({name: 'zhangsan', age: {$gte: 18}}, (error, document) => console.log('05 == ', error, document))

// 只显示 name 和 age 字段，且不显示 _id（在字段前面加 - 号），还可以用对象写法：{_id: 0, name: 1, age: 1}
StudentModel.find({name: 'zhangsan'}, '-_id name age', (error, document) => console.log('06 == ', error, document))

// 第三个参数传递选项
StudentModel.find({name: 'zhangsan'}, null, {skip: 1, limit: 3}, (error, document) => console.log('07 == ', error, document))

// 只返回一条数据
StudentModel.findOne({name: 'zhangsan'}, (error, document) => console.log('08 == ', error, document))

// ************************************************ 修改数据 ************************************************
// 把年龄大于 18 的名称都改成 aaa，修改全部
StudentModel.update({age: {$gt: 18}}, {name: 'aaa'}).then(result => console.log('09 == ', result))

// 把年龄大于 18 的名称都改成 aaa，修改一个
StudentModel.updateOne({age: {$gt: 18}}, {name: 'aaa'}).then(result => console.log('10 == ', result))

// 把年龄大于 18 的名称都改成 aaa，修改全部
StudentModel.updateMany({age: {$gt: 18}}, {name: 'aaa'}).then(result => console.log('11 == ', result))

// ************************************************ 删除数据 ************************************************
// 把年龄等于 18 的文档删除掉，删除全部
StudentModel.remove({age: {$eq: 18}}).then(result => console.log('12 == ', result))

// 把年龄等于 18 的文档删除掉，删除一个
StudentModel.deleteOne({age: {$eq: 18}}).then(result => console.log('13 == ', result))

// 把年龄等于 18 的文档删除掉，删除全部
StudentModel.deleteMany({age: {$eq: 18}}).then(result => console.log('14 == ', result))
```

### 3. Document

通过 find() 查询的结果，返回的对象，就是 Document 文档对象。

Document 对象是 Model 对象的实例。

```js
// ************************************************ 创建文档 ************************************************
// 创建一个文档
const studentDocument = new StudentModel({
  name: 'wangwu',
  age: 17,
  gender: '男'
})

// 将文档保存到数据库
studentDocument.save().then(result => console.log('15 ==', result))

StudentModel.findOne({}, (error, document) => {
  console.log('16 == ', error, document)

  // 获取当前文档的 _id
  console.log('document.id：', document.id)

  // 将当前文档转换成一个 json 对象返回
  console.log('document.toJSON()：', document.toJSON())

  // 将当前文档转换成一个普通 js 对象返回，所有的 Document 对象的方法和属性都不能使用了
  console.log('document.toObject()：', document.toObject())

  // 修改当前文档的 name 为 bbb
  document.update({name: 'bbb'}).then(result => console.log('17 == ', result))

  // 修改当前文档的 age 为 15
  document.age = 15
  document.save()

  // 删除当前文档
  document.remove()
})
```

