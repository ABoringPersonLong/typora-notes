# Mac：

官网下载 .dmg 直接安装。

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

