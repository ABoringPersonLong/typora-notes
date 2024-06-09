# mac：

官网下载后解压放到：/Library/Java/JavaVirtualMachines/jdk-17.0.11.jdk

打开 .bash_profile 文件：

```bash
open -e .bash_profile
```

将环境变量添加进去：

```bash
# Java
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-17.0.11.jdk/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH:.
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:.
```

保存：

```bash
source .bash_profile
```

查看版本：

```bash
java -version
```
