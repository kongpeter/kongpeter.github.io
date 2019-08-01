---
layout:     post   				    # 使用的布局（不需要改）
title:      Mac OS 配置 java 环境变量 				# 标题 
subtitle:   java 环境变量配置 #副标题
date:       2019-8-01 				# 时间
author:     Lingxuan Kong 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags: 								#标签
    - Java
    - macOS
---

## 1.下载 JDK

JDK 的安装包可以直接从官网下载,但是现在好像必须要注册账号才能下载了. 那就注册一个吧,反正也不浪费时间.

下载地址: [官方网站](https://link.juejin.im/?target=http%3A%2F%2Fwww.oracle.com%2Ftechnetwork%2Fjava%2Fjavase%2Fdownloads%2Findex.html)

版本的选择必须是 MAC OS, 记得一定要勾选同意, 否则无法下载. 



## 2. 安装 JDK

下载下来的安装包是 DMG,直接双击安装即可.

安装完成之后，打开终端（在搜索里面直接输入，terminal）：

然后在终端里面输入：

```
java -version
```

如果显示：

```
java version "1.8.0_221"
Java(TM) SE Runtime Environment (build 1.8.0_221-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.221-b11, mixed mode)
```

则表示已经安装成功。接下来就可以配置环境变量了。



## 3.配置环境变量

### 1.检查 JDK 安装的路径

```linux
# 进入 JDK 安装的盘符，如果没有更改，都是默认的盘符
cd /usr/libexec/
# 输入如下代码，注意 V 是大写
./java_home -V
```

输入以上输入正确，应当输出以下结果：

```
Matching Java Virtual Machines (1):
    1.8.0_221, x86_64:	"Java SE 8"	/Library/Java/JavaVirtualMachines/jdk1.8.0_221.jdk/Contents/Home

/Library/Java/JavaVirtualMachines/jdk1.8.0_221.jdk/Contents/Home
```

其中：

**/Library/Java/JavaVirtualMachines/jdk1.8.0_221.jdk/Contents/Home**

就是你的 JDK 安装路径，记下来，待会要用的。

### 2.配置PATH和CLASSPATH

```
# 用管理员权限打开配置文件
sudo vim /etc/profile
# 密码不会显示，只管输入就好
password: xxxxxxx

# 点击 i 进入编辑模式，输入如下三行代码：
JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk-10.0.2.jdk/Contents/Home"
CLASS_PATH="$JAVA_HOME/lib"
PATH=".:$PATH:$JAVA_HOME/bin"

# 然后按 ESC 退出编辑模式，然后输入下一行代码强制保存
:wq!

# 输入下一行代码，使配置生效
source /etc/profile
```

### 3.查看环境变量

```
# 输入如下代码，查看环境变量
echo $JAVA_HOME
echo $PATH
echo $CLASS_PATH
```



## 4.测试

```
# 先测试编译 java，在终端中输入如下代码：
javac

# 如果出现如下代码，则说明安装成功：
用法: javac <options> <source files>
其中, 可能的选项包括:
  -g                         生成所有调试信息
  -g:none                    不生成任何调试信息
  -g:{lines,vars,source}     只生成某些调试信息
  -nowarn                    不生成任何警告
  -verbose                   输出有关编译器正在执行的操作的消息
  -deprecation               输出使用已过时的 API 的源位置
  -classpath <路径>            指定查找用户类文件和注释处理程序的位置
  -cp <路径>                   指定查找用户类文件和注释处理程序的位置
  -sourcepath <路径>           指定查找输入源文件的位置
  -bootclasspath <路径>        覆盖引导类文件的位置
  -extdirs <目录>              覆盖所安装扩展的位置
  -endorseddirs <目录>         覆盖签名的标准路径的位置
  -proc:{none,only}          控制是否执行注释处理和/或编译。
  -processor <class1>[,<class2>,<class3>...] 要运行的注释处理程序的名称; 绕过默认的搜索进程
  -processorpath <路径>        指定查找注释处理程序的位置
  -parameters                生成元数据以用于方法参数的反射
  -d <目录>                    指定放置生成的类文件的位置
  -s <目录>                    指定放置生成的源文件的位置
  -h <目录>                    指定放置生成的本机标头文件的位置
  -implicit:{none,class}     指定是否为隐式引用文件生成类文件
  -encoding <编码>             指定源文件使用的字符编码
  -source <发行版>              提供与指定发行版的源兼容性
  -target <发行版>              生成特定 VM 版本的类文件
  -profile <配置文件>            请确保使用的 API 在指定的配置文件中可用
  -version                   版本信息
  -help                      输出标准选项的提要
  -A关键字[=值]                  传递给注释处理程序的选项
  -X                         输出非标准选项的提要
  -J<标记>                     直接将 <标记> 传递给运行时系统
  -Werror                    出现警告时终止编译
  @<文件名>                     从文件读取选项和文件名
```

```
# 执行 java 文件
java

# 如果出现如下代码，则说明安装成功：
用法: java [-options] class [args...]
           (执行类)
   或  java [-options] -jar jarfile [args...]
           (执行 jar 文件)
其中选项包括:
    -d32	  使用 32 位数据模型 (如果可用)
    -d64	  使用 64 位数据模型 (如果可用)
    -server	  选择 "server" VM
                  默认 VM 是 server,
                  因为您是在服务器类计算机上运行。


    -cp <目录和 zip/jar 文件的类搜索路径>
    -classpath <目录和 zip/jar 文件的类搜索路径>
                  用 : 分隔的目录, JAR 档案
                  和 ZIP 档案列表, 用于搜索类文件。
    -D<名称>=<值>
                  设置系统属性
    -verbose:[class|gc|jni]
                  启用详细输出
    -version      输出产品版本并退出
    -version:<值>
                  警告: 此功能已过时, 将在
                  未来发行版中删除。
                  需要指定的版本才能运行
    -showversion  输出产品版本并继续
    -jre-restrict-search | -no-jre-restrict-search
                  警告: 此功能已过时, 将在
                  未来发行版中删除。
                  在版本搜索中包括/排除用户专用 JRE
    -? -help      输出此帮助消息
    -X            输出非标准选项的帮助
    -ea[:<packagename>...|:<classname>]
    -enableassertions[:<packagename>...|:<classname>]
                  按指定的粒度启用断言
    -da[:<packagename>...|:<classname>]
    -disableassertions[:<packagename>...|:<classname>]
                  禁用具有指定粒度的断言
    -esa | -enablesystemassertions
                  启用系统断言
    -dsa | -disablesystemassertions
                  禁用系统断言
    -agentlib:<libname>[=<选项>]
                  加载本机代理库 <libname>, 例如 -agentlib:hprof
                  另请参阅 -agentlib:jdwp=help 和 -agentlib:hprof=help
    -agentpath:<pathname>[=<选项>]
                  按完整路径名加载本机代理库
    -javaagent:<jarpath>[=<选项>]
                  加载 Java 编程语言代理, 请参阅 java.lang.instrument
    -splash:<imagepath>
                  使用指定的图像显示启动屏幕
有关详细信息, 请参阅 http://www.oracle.com/technetwork/java/javase/documentation/index.html。
```

