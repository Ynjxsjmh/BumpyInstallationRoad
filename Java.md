<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-generate-toc again -->
**Table of Contents**

- [Windows](#windows)
    - [安装 JDK](#安装-jdk)
    - [配置环境变量](#配置环境变量)

<!-- markdown-toc end -->


# Windows

<https://blog.csdn.net/yx1214442120/article/details/55099213>

## 安装 JDK


## 配置环境变量
打开环境变量配置。计算机→属性→高级系统设置→高级→环境变量，在系统变量中配置。

1. 创建三个 JAVA_HOME。
   - JAVA_HOME，如果需要 1.7 版本变量值设为 `%JAVA7_HOME%`；如果需要 1.8 版本变量值设为 `%JAVA8_HOME%`，便于切换。
   - JAVA7_HOME，存放 JDK1.7 的安装路径。例如 `C:\Program Files\Java\jdk1.7.0_45`
   - JAVA8_HOME，存放 JDK1.8 的安装路径。例如 `C:\Program Files\Java\jdk1.8.0_144`

2. 配置 CLASSPATH。

   新建变量 `CLASSPATH`，变量值设为 `.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar;`（第一个分号前前面有一个点）。
   
   ps. `.` 表示当前路径，表示也要在当前路径下搜索。

3. 配置 Path。

   在 Path 变量值中加入 `%JAVA_HOME%\bin;% JAVA_HOME%\jre\bin;`

4. 在安装 JDK1.8 时（我的电脑是先安装 jdk1.6 再安装的 jdk1.8），会将 java.exe、javaw.exe、javaws.exe 三个可执行文件复制到了 C:\Windows\System32 目录，这个目录在 WINDOWS 环境变量中的优先级高于 JAVA_HOME 设置的环境变量优先级，所以要将这个目录中这三个文件删除。

5. 验证

   命令行里输入 `java -version`

