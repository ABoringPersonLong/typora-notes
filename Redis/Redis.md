# mac安装：

官网下载最新稳定版后改名为 redis 后解压放到：/usr/local/redis

切换到对应目录：

```bash
cd /usr/local/redis
```

编译测试：

```bash
sudo make test
```

编译安装：

```bash
sudo make install
```

ok，**不需要配环境变量**

启动服务端：

```bash
redis-server
```

查看服务是否启动：

```bash
# 查看 redis 进程的 pid
pgrep redis
```

客户端连接服务端：

```bash
redis-cli -h 127.0.0.1 -p 6379
```

命令操作：

```
1.redis 的数据结构：
    redis 存储的是 key,value 格式的数据，其中 key 都是字符串，value 有 5 中不同的数据结构
    value 的数据结构：
        1.字符串类型 string
        2.哈希类型 hash：Map 格式
        3.列表类型 list：LinkedList 格式，可以重复元素
        4.集合类型 set：HashSet 格式，不可以重复元素
        5.有序集合类型 sortedset：可以排序的集合
2.字符串类型：string
    1.存储：set key value
    2.获取：get key
    3.删除：del key
3.哈希类型：hash
    1.存储：hset key field value
    2.获取：hget key field
    3.删除：hdel key field
    4.获取所有：hgetall key
4.列表类型：list，可以添加一个元素到列表的头部(左边)或者尾部(右边)
    1.存储：
        lpush key value：将元素加入列表左边
        rpush key value：将元素加入列表右边
    2.获取：
        lrange key start stop：范围获取
        lrange key 0 -1：获取全部
    3.删除：
        lpop key：删除列表最左边的元素，并将元素返回
        rpop key：删除列表最右边的元素，并将元素返回
5.集合类型：set 不允许重复
    1.存储：sadd key member
    2.获取：smembers key：获取集合中所有元素
    3.删除：srem key member：删除集合中的某个元素
6.有序集合类型：sortedset 不允许重复元素，且元素有顺序
    1.存储：zadd key score member
        score 是一个用来排序的数字，从小到大排序
    2.获取：
        zrange key start stop：范围获取，不会获取 score
        zrange key start stop withscores：范围获取，会获取 score
        zrange key 0 -1：获取全部
    3.删除：zrem key member
7.通用命令：
    1.keys *：查询所有的键
    2.type key：获取键对应的 value 的类型
    3.flushdb：删除当前数据库中的所有 Key
    4.flushall：删除所有数据库中的 key
```

