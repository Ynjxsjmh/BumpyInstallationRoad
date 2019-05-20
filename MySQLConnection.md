<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-generate-toc again -->
**Table of Contents**

- [Dev 连接 MySQL 数据库](#dev-连接-mysql-数据库)
    - [生成 libmysql.a](#生成-libmysqla)
    - [DEV 编译器选项配置](#dev-编译器选项配置)
    - [测试代码](#测试代码)
    - [可能出现的问题](#可能出现的问题)
        - [undefined reference to `mysql_init@4'](#undefined-reference-to-mysqlinit4)
        - [mysql.h	[Error] 'SOCKET' does not name a type](#mysqlh	error-socket-does-not-name-a-type)

<!-- markdown-toc end -->

# Dev 连接 MySQL 数据库
## 生成 libmysql.a
首先下载一下 MinGW 工具包，地址 https://sourceforge.net/projects/mingw/files/MinGW/Extension/mingw-utils/ ，我用的是 0.3 的。如果不想下载，可以在该 repo 的 resource 文件夹下找到。

我们用到的是这个工具包里面的 reimp.exe

然后需要两步来生成 libmysql.a

1. 在 `D:\SoftWare\MySQL\MySQL Server 5.6\lib` 里运行 `path\to\reimp.exe -d libmysql.lib` 得到 `libmysql.def` 文件
2. 然后在同样的目录下运行 `"C:\Program Files (x86)\Dev-Cpp\MinGW64\bin\dlltool.exe" -k -d libmysql.def -l libmysql.a` 就可以生成 `libmysql.a` 了

**注意：**上面我用的都是我的路径，列位看官需要根据自己的实际情况来改。其中的 `dlltool.exe` 可以在 Dev-Cpp 安装路径下的 `MinGW64\bin` 下找到

我们还需要将生成的 `libmysql.a` 复制到 Dev-CPP 的安装目录下的 lib 文件夹里面（这一步的目的是让 Dev 的编译器能够找到它，所以放在哪里无所谓，只要能找到。放在这里是因为默认会往这个文件夹里找）。比如，我的就是 `C:\Program Files (x86)\Dev-Cpp\MinGW64\lib`

最后我们需要将 `D:\SoftWare\MySQL\MySQL Server 5.6\lib\libmysql.dll` 这个文件放到 `C:\Windows\Systm32`（32 位）或者 `C:\Windows\SysWOW64`（64 位）这两个目录中的一个即可

## DEV 编译器选项配置
打开 Dev-CPP 的任务栏的 `工具--编译选项`

1. 选中`编译器`选项卡，在**在连接器命令行加入以下命令**中加入 `-lmysql`

   ![配置 DEV 的连接器](./img/MySQLConnection/dev-linker.jpg)

2. 选中`目录`选项卡中的`C++ 包含文件`，在其中加入 `D:\SoftWare\MySQL\MySQL Server 5.6\include`

   ![配置 DEV 的目录](./img/MySQLConnection/dev-include.jpg)

## 测试代码
运行之前列位看官得改下的用户名密码啥的。下面那个 `crm` 是我数据库的一个表，列位看官们最好改成自己数据库里有的一个表名

```c
#include <stdio.h>
#include <winsock2.h>
#include <mysql.h>

int main()
{
	MYSQL mysql;
	mysql_init( &mysql );

	if ( !mysql_real_connect( &mysql, "localhost", "root", "root", "crm", 3306, NULL, 0 ) )
	{
		printf( "\nconnect error!" );
	} else   {
		printf( "\nconnect success!\n" );
	}

	mysql_close( &mysql );

	return(0);
}
```

当然这里只是一个最简单的判断数据库是否连接上的代码，具体如何操作数据库这里就没有涉及。

## 可能出现的问题
### undefined reference to `mysql_init@4'

```c
undefined reference to `mysql_init@4'
undefined reference to `mysql_real_connect@32'
undefined reference to `mysql_close@4'
```

出现这个问题很可能是你啥都没做就运行测试代码了或者没有加上 `-lmysql`

### mysql.h	[Error] 'SOCKET' does not name a type

得加上 `#include <winsock2.h>`，因为 `SOCKET` 是其中定义的一个类型

