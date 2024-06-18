# Mac：

官网下载 8.0 的最高版本的 .dmg 直接安装。

打开 .bash_profile 文件：

```bash
open -e .bash_profile
```

将环境变量添加进去：

```bash
# MySQL
export PATH=${PATH}:/usr/local/mysql/bin
```

保存：

```bash
source .bash_profile
```

登陆：

```
mysql -uroot -padministrator
```

启动 mysql 服务：

```bash
sudo /usr/local/mysql/support-files/mysql.server start
```

停止 mysql 服务：

```bash
sudo /usr/local/mysql/support-files/mysql.server stop
```

重启 mysql 服务：

```bash
sudo /usr/local/mysql/support-files/mysql.server restart
```
