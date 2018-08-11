## Oracle自治事务处理云服务抢先体验2--连接ATP实例


Oracle自治事务处理云服务抢先体验系列：

[Oracle自治事务处理云服务抢先体验1：创建ATP实例](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/atp-provisioning-1.md)

[Oracle自治事务处理云服务抢先体验2：连接ATP实例](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/atp-connecting-1.md)

[Oracle自治事务处理云服务抢先体验3：向ATP数据库中加载数据](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/atp-loading-1.md)




**访问ATP实例**


访问ATP实例的方式有多种，如：

- Connect SQL*Plus Connect 
- SQLcl Connect 
- SQL Developer 
- Connect with JDBC Thin Driver 


**本文将介绍使用Oracle SQL Developer工具来访问ATP实例。**

Oracle SQL Developer工具是数据库管理员和数据库开发人员的最爱，它不光好用，还是免费的。访问ATP，对SQL Developer的版本有要求，版本太低了是不行的，毕竟ATP是一个很炫酷的东西，总得矜持一点吧，不是哪个随便的工具就可以访问的。最低版本是多少呢？ 我也不知道，文档上没有说，我只知道有一个18.2.0以上的版本肯定是没问题的，今天就介绍18.2以上的版本，其他的版本，你们自己研究去。

最新版 SQL Developer下载地址下面，找到最新版的，下载下来就是了，注意：最好选带JDK的（如：Windows 64-bit with JDK 9 included）。

下载链接：[SQL Developer](https://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html)

工具下载下来后，无需安装，直接打开（就是这么任性），右键点击左上角“连接”按钮，选择“新建连接”。


《图1》
![**<图片1>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Connecting/1.png)

配置数据库连接。

《图2》
![**<图片2>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Connecting/2.png)

**需要配置：**

**连接名**：名称而已。

**用户名**：ATP数据库管理员，ADMIN（你没得选）。

**密码**：ADMIN用户的口令（你自己设置的，别忘记了）。

**连接类型**： 选“云PDB”或者"Cloud PDB"。

**配置文件**：重点来了，前面下载的客户端信任文件，在这里用上了，在“浏览”中找到信任文件的位置，打开即可。

**服务**：上面的客户端信任文件选择后，就会出现一个下拉服务列表，选择“**数据库名_medium**”的服务。

配置完成，先测试一下，测试通过后，点击连接，顺利的连接到ATP实例。如图。

《图3》
![**<图片3>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Connecting/3.png)



**在ATP库中创建应用程序用户**


ADMIN用户是管理员用户，主要用来管理ATP数据库，我们应该为应用程序单独创建用户，来存取应用数据集。

下面演示，在SQL Developer的工作表中执行以下语句，创建应用程序用户atpc_user，并授予角色dwrole。

	create user atpc_user identified by "Q1w2e3r4#Q1w2e3r4#";
	grant dwrole to atpc_user;
	

《图4》
![**<图片4>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Connecting/4.png)


 
**注意**：ATP数据库中已经预定义了角色DWROLE，这个角色提供了一个数据库用户比较常用的权限。角色DWROLE具有以下权限：

	CREATE ANALYTIC VIEW, 
	CREATE ATTRIBUTE DIMENSION, 
	ALTER SESSION, 
	CREATE HIERARCHY, 
	CREATE JOB, 
	CREATE MINING MODEL, 
	CREATE PROCEDURE, 
	CREATE SEQUENCE, 
	CREATE SESSION, 
	CREATE SYNONYM, 
	CREATE TABLE, 
	CREATE TRIGGER, 
	CREATE TYPE, 
	CREATE VIEW, READ,WRITE ON directory DATA_PUMP_DIR, 
	EXECUTE privilege on the PL/SQL package DBMS_CLOUD



应用程序用户atpc_user创建完成后，我们来演示，用SQL Developer工具在用户aptc_user下创建SH相关表。

**在SQL Developer中新建一个数据库连接**

创建一个以用户atpc_user登录的数据库连接。点击连接。

《图5》
![**<图片5>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Connecting/5.png)




**在ATP数据库中创建SH相关表**

注：SH即Sales History，是Oracle数据库中的sample schema。在本例中，我们将在用户atpc_user下创建SH相关表，并在下一篇文章中介绍，将外部数据加载到ATP数据库中的SH表中。

首先，通过以下链接，下载[SH表创建脚本](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/scripts/sql_%20commands_to_create_sh_tables_in_atpc_user.txt)。

在SQL Developer的工作表中将SH表创建脚本打开，执行。

《图6》
![**<图片6>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Connecting/6.png)


检查脚本输出内容，确认所有表是否创建成功。

《图7》
![**<图片7>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Connecting/7.png)


另外，我们也可以通过SQL Developer工具查看相关表的信息。


《图8》
![**<图片8>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Connecting/8.png)


点击其中的某张表，查看这张表的列信息，如图：

《图9》
![**<图片9>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Connecting/9.png)



