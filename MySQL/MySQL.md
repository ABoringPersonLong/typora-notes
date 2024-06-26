# Mac：

官网下载 8.0 的最高版本的 .dmg 直接安装。

## 配置环境变量（好像不用）

打开`bash shell`和`zsh shell`的环境变量文件：

```bash
open -e ~/.bash_profile
open -e ~/.zshrc
```

将环境变量添加进去：

```bash
# MySQL
export PATH=${PATH}:/usr/local/mysql/bin
```

保存：

```bash
source ~/.bash_profile
source ~/.zshrc
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
