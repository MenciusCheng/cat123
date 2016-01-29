Windows 下安装 MySQL 解压版
===========================

教程版本：MySQL 5.7.10 64位

参考资料：[Installing MySQL on Microsoft Windows Using a noinstall Zip Archive](http://dev.mysql.com/doc/refman/5.7/en/windows-install-archive.html)

下载地址：[Download MySQL Community Server](http://dev.mysql.com/downloads/mysql/)

解压文档与配置路径
------------------

1. 把压缩文档解压在路径`C:\Program Files\MySQL\`下。（此时我的MySQL安装目录为`C:\Program Files\MySQL\mysql-5.7.10-winx64`）

2. 设置环境变量：打开`系统 -> 高级系统设置 -> 环境变量`，修改变量`Path`，添加路径`C:\Program Files\MySQL\mysql-5.7.10-winx64\bin`。

创建配置文件与初始化
--------------------

1. 在安装目录下创建一个文件my.ini（也可以通过复制my-default.ini），并添加下面配置 ：

```
[mysqld]
# 设置 basedir 为你的安装路径
basedir=C:\\Program Files\\MySQL\\mysql-5.7.10-winx64
# 设置 datadir 为你的数据库目录
datadir=C:\\Program Files\\MySQL\\data
```

2. 以管理员身份打开命令提示符，运行以下命令：

```
C:\WINDOWS\system32> cd C:\Program Files\MySQL\mysql-5.7.10-winx64\bin
C:\Program Files\MySQL\mysql-5.7.10-winx64\bin> mysqld --initialize --console
```

> 注：
> `--initialize`选项会生成一个随机密码的root账号，改用`--initialize-insecure`选项则会生成一个密码为空的root账号。
> `--console`选项是为了能在命令提示符中打印信息。注意，这里会打印生成的随机密码。
> 你也可以指定配置文件位置`mysqld --defaults-file=C:\my.ini --initialize`。注意，这里`--defaults-file`选项必须放在第一位。

3. 目录生成成功后，再次运行`mysqld`或`mysql --console`启动 MySQL 服务。

4. 连接 MySQL 服务。新建命令提示符，运行以下命令：

```
C:\WINDOWS\system32> mysql -u root -p
Enter password: (把刚才生成的随机密码输入到这里)
```

5. 如果你是使用`--initialize-insecure`选项，则应该运行以下命令：

```
C:\WINDOWS\system32> mysql -u root --skip-password
```

6. 连接成功后，修改root账号密码：

```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
```

注册 MySQL 为 Windows 服务
--------------------------

1. 注册 Windows 服务前，先要停止 MySQL 服务，通过运行以下命令：

```
C:\> "C:\Program Files\MySQL\mysql-5.7.10-winx64\bin\mysqladmin" -u root shutdown
```

2. 再用以下命令注册服务（注意，这里最好用全路径）：

```
C:\> "C:\Program Files\MySQL\mysql-5.7.10-winx64\bin\mysqld" --install
```

3. 注册成功后，每次开机就可以自动启动 MySQL 服务了。

4. 可以通过命令`NET START MySQL`来手动开启 MySQL 服务，和命令`NET STOP MySQL`停止。

5. 想要移除 MySQL 服务，先停止 MySQL 服务，再运行以下命令：

```
C:\> "C:\Program Files\MySQL\mysql-5.7.10-winx64\bin\mysqld" --remove
```