## Oracle自治事务处理云服务抢先体验2--连接ATP实例





[Connecting SQL Developer to Autonomous Transaction Processing](http://www.oracle.com/webfolder/technetwork/tutorials/obe/cloud/atp/OBE_Connecting%20SQL%20Developer%20to%20Autonomous%20Transaction%20Processing/connecting_sql_developer_to_autonomous_transaction_processing.html)

#**访问ATP实例**

可以用多种方式访问ATP，如：


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
![**<图片1>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/connecting/1.png)

配置数据库连接。

《图2》
![**<图片2>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/connecting/2.png)

**需要配置：**

**连接名**：名称而已。

**用户名**：ATP数据库管理员，ADMIN（你没得选）。

**密码**：ADMIN用户的口令（你自己设置的，别忘记了）。

**连接类型**： 选“云PDB”或者"Cloud PDB"。

**配置文件**：重点来了，前面下载的客户端信任文件，在这里用上了，在“浏览”中找到信任文件的位置，打开即可。

**服务**：上面的客户端信任文件选择后，就会出现一个下拉服务列表，选择“数据库名_medium”的服务。

配置完成，先测试一下，测试通过后，点击连接，顺利的连接到ATP实例。如图。

《图3》
![**<图片3>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/connecting/3.png)

http://www.oracle.com/webfolder/technetwork/tutorials/obe/cloud/atp/obe_provisioning%20autonomous%20transaction%20processing/provisioning_autonomous_transaction_processing.html

#Create a User in your Autonomous Transaction Processing Database
**在ATP库中创建应用程序用户**

在SQL Developer的工作表中执行以下语句，创建应用程序用户atpc_user，并授予角色dwrole。

	create user atpc_user identified by "Q1w2e3r4#Q1w2e3r4#";
	grant dwrole to atpc_user;
	

《图4》
![**<图片4>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/connecting/4.png)



Note: Autonomous Transaction Processing databases come with a pre-defined database role named DWROLE. 
This role provides the common privileges for a database user: 

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



关于角色DWROLE，

#在SQL Developer中新建一个数据库连接
创建一个以用户atpc_user登录的数据库连接。点击连接。

《图5》
![**<图片5>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/connecting/5.png)

https://docs.oracle.com/en/cloud/paas/atp-cloud/atpug/getting-started.html#GUID-00645C09-4E76-44C6-8BBE-B433D501AADB



http://www.oracle.com/webfolder/technetwork/tutorials/obe/cloud/atp/OBE_Connecting%20SQL%20Developer%20to%20Autonomous%20Transaction%20Processing/connecting_sql_developer_to_autonomous_transaction_processing.html

#Create SH Tables in your Autonomous Transaction Processing Database
在ATP数据库中创建SH表（）
After you have connected SQL Developer to your Autonomous Transaction Processing database, use a SQL Developer worksheet to define CREATE TABLE statements to create the SH tables (sales history tables from an Oracle sample schema) in the atpc_user schema. In the next tutorial, you will load data into these tables from an object store.  


《图6》
![**<图片6>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/connecting/6.png)



#Examine the SH Tables that you Created
检查脚本输出内容，确认所有表是否创建成功。

《图7》
![**<图片7>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/connecting/7.png)

Note that the new tables also appear in the SQL Developer Connections panel.

《图8》
![**<图片8>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/connecting/8.png)

Examine the details of each column of the CHANNELS table. 

《图9》
![**<图片9>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/connecting/9.png)



