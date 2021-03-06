## 准备工作
### 创建账户
1. 登录 [TDSQL 控制台](https://console.cloud.tencent.com/dcdb)，选择所需实例，单击实例名或操作列的【管理】，进入实例管理页面。
2. 选择【账号管理】页，单击【创建账号】。
![](https://main.qcloudimg.com/raw/148943eb024c9d3871b3c5d509de2e20.png)
3. 在弹出的对话框，输入账号名、主机、密码、备注，确认无误后单击【确认】。
主机名实际是网络出口地址，支持%的匹配方式，代表所有 IP 均可访问。
![](https://main.qcloudimg.com/raw/9eed6bea2c606347767f6821e3dc2eb5.png)
4. 进入修改权限对话框，根据需求分配权限后，单击【保存设置】即可完成权限分配。若需稍后设置权限，单击【之后设置】即可。
左边导航栏提供完全兼容 MySQL 管理方式的图形化界面，权限管理可以细化到列级。
![](https://main.qcloudimg.com/raw/4a6bdfb7e48222945440db418e7f6de1.png)
5. 返回账号列表，单击【修改权限】可以修改用户权限，单击【克隆账号】可以完全复制当前账号权限来新建一个帐号，单击【更多】可以重置密码和删除账号。
![](https://main.qcloudimg.com/raw/f72d3815f500b0c5a4e7e8d699ec793f.png)

### 获取外网地址
1. 进入实例详情页，在基本信息的外网地址栏，单击【开启】。
![](https://main.qcloudimg.com/raw/71a29582f85cbda585ed586341f9b351.png)
2. 开启后，获取外网地址和端口号。TDSQL 提供了唯一的 IP、端口供用户访问和使用。

## 连接步骤
创建账户和获取外网地址后，可通过第三方工具和程序驱动进行连接 TDSQL。
- Windows 端，以命令行连接、客户端连接和 JDBC 驱动连接三种方式为例。
- Linux 端，以命令行连接为例。

### Windows 命令行连接
1. 打开 Windows 命令行，在 MySQL 的正确路径下输入以下命令。
```
mysql -h外网地址 -P端口号 -u用户名  -p
Enter password: **********（输入密码）
```
2. 将相关代码正确输入后，显示如下信息，成功连接数据库，下一步即可进行数据库内相关操作。
```
Welcome to the MySQL monitor.  Commands end with ; or \g.
```
		
### Windows 客户端连接
1. 下载一个标准的 SQL 客户端，例如 MySQL Workbench 、SQLyog 等，本文以 SQLyog 为例。
2. 打开 SQLyog，选择【文件】>【新连接】，输入对应的主机地址、端口、用户名和密码，单击【连接】。
 - 我的SQL主机地址：输入前面获得的外网地址。
 - 用户名：输入前面创建的账户名。
 - 密码：输入账户对应的密码。
 - 端口：输入外网地址对应的端口。
![](https://main.qcloudimg.com/raw/56645ca6d1c5fe7803e05f7643b833ae.png)
3. 连接成功页面如下图所示，在此页面即可进行数据库内相关操作。
![](https://main.qcloudimg.com/raw/1f492c179e2f604afc02a775d58a2d9c.png)

### Windows JDBC 驱动连接
TDSQL 支持程序驱动连接，本文以 Java 使用 JDBC Driver for MySQL (Connector/J) 连接 TDSQL 为例。

1. 在 [MySQL 官网](https://dev.mysql.com/downloads/connector/j/5.0.html) 下载一个 JDBC 的 jar 包，将其导入 Java 引用的 Library 中。
2. 调用 JDBC 代码如下：
```
		public static final String url = "外网地址";
		public static final String name = "com.mysql.jdbc.Driver"; //调用 JDBC 驱动
		public static final String user = "用户名";
		public static final String password = "密码";
		//JDBC
		Class.forName("com.mysql.jdbc.Driver"); 
				Connection conn=DriverManager.getConnection("url, user, password");
		//
		conn.close();
```
3. 连接成功后，下一步即可进行其他数据库内操作。
>因 TDSQL 在分表和插入数据时需要标记 shardkey，所以无法用 JDBC 调用这些操作。

### Linux 命令行连接
以腾讯云服务器中 CentOS 7.2 64 位系统为例，云服务器购买请参见 [购买方式](https://intl.cloud.tencent.com/document/product/213/506)。
1. 登录 Linux 后，输入命令 `yum install mysql`，利用 CentOS 自带的包管理软件 Yum 在腾讯云镜像源中下载安装 MySQL 客户端。
![](https://main.qcloudimg.com/raw/fe1470a47fd3311460a7cfd24f70a88a.png)
2. 命令行显示 complete 后，表示 MySQL 客户端安装完成。
3. 输入命令 `mysql -h外网地址 -P端口 -u用户名 -p` 连接 TDSQL，下一步即可进行分表操作。
下图以`show databases;`为例。
![](https://main.qcloudimg.com/raw/c094ba46f8a3d321ad4a199d88d9d3e6.png)

