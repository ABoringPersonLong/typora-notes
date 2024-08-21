# Mac：

官网下载后解压放到：/Library/Java/JavaVirtualMachines/jdk-17.0.11

## 配置环境变量（好像不用）

打开`bash shell`和`zsh shell`的环境变量文件：

```bash
open -e ~/.bash_profile
open -e ~/.zshrc
```

将环境变量添加进去：

```bash
# Java
export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-22.0.1/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH:.
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:.
```

保存：

```bash
source ~/.bash_profile
source ~/.zshrc
```

查看版本：

```bash
java -version
```
