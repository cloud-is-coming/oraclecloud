# Oracle MySQL云服务入门系列1：创建MySQL实例
关于Oracle MySQL 云服务的介绍，参见官方网站介绍：[Oracle MySQL 云服务](https://cloud.oracle.com/zh_CN/mysql)。

《Oracle MySQL云服务入门系列》包含以下内容：

1. 创建MySQL实例


1. 访问MySQL实例


1. MySQL实例生命周期管理


1. MySQL自动备份和恢复


1. MySQL企业监控

本文为Oracle MySQL云服务入门系列第一篇：创建MySQL实例。将详细介绍如何在Oracle云上，通过图形界面快速创建一个MySQL实例。



**通过浏览器登录Oracle云主页**

在浏览器地址栏输入Oracle云主页地址：[https://cloud.oracle.com](https://cloud.oracle.com)

点击“Sign In”，


![**<图片1>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/provisioning/1.jpg)

在“Select Account Type”下拉框中选择“Cloud Account with Identity Cloud Service”,在“Cloud Account Name”文本输入框中，输入云账号名称，然后点击“My Services”按钮，进入登录界面。

![**<图片2>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/provisioning/2.jpg)

在用户认证界面，输入用户名和口令，点击登录

![**<图片3>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/provisioning/3.jpg)

在云服务主界面，点击左上角的下拉菜单按钮，在主界面左侧会出现菜单，点击“服务”按钮，在展开的服务列表中选择“MySQL”,进入MySQL云服务主界面。如图：

![**<图片4>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/provisioning/4.jpg)

在MySQL云服务主界面，点击“Create Instance”按钮，进入MySQL实例配置助手，如图：

![**<图片5>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/provisioning/5.jpg)


输入实例概要信息，如实例名、实例描述、通知邮箱等，点击“下一步”：

![**<图片6>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/provisioning/6.jpg)

在实例详细配置界面，输入MySQL相关配置信息。

**设置Configure**

**1 Compute Shape**：在下拉菜单选择“OC3-1.0 OCPU and 7.5 GB RAM”

**2 SSH Public Key**：点击Edit按钮，在本地目录上选择一个ssh公钥。需要说明一下，MySQL云服务中创建好的MySQL实例对外已经提供了访问端口，缺省3306（可自行修改），应用程序或开发工具可以通过该端口访问MySQL数据库，用户只需要使用MySQL服务，而无需管理服务的基础设施，这也是PaaS服务相比于IaaS服务的最大特点：用户只需要关注服务本身，底层的基础设施完全交给云服务商。即便如此，Oracle还是很人性化的为用户提供了另一个选择：用户可以拥有实例操作系统的root权限，对根据需要，执行操作系统级的操作。为了安全考虑，用户只能使用SSH 密钥对的方式，通过22端口访问实例的操作系统。设置“SSH公共密钥”步骤中，需要用户上传一个SSH公钥。

**3 User High Performance Storage**：缺省情况下，MySQL实例的磁盘为普通磁盘，不过Oracle也提供了SSD高性能固态盘选项，勾选此选项，系统将选择使用高性能固态盘来创建MySQL实例。


![**<图片7>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/provisioning/7.jpg)

**设置“MySQL Configuration”**

**第1部分**是设置MySQL实例本身，包括数据库存储空间、root用户口令、Schema名称、字符集、时区和端口。

**第2部分**是设置MySQL企业监控器（Enterprise Monitor），其中：
Manager User：监控用户名和口令
Agent User： 监控代理用户名和口令

![**<图片8>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/provisioning/8.jpg)

**设置“Backup and Recovery Configuration”**

在第1部分的“Backup Destination”下拉菜单中，选择“Both Cloud and Disk Storage”，即将备份同时存放在本地盘和云对象存储中。 由于选择了同时存放在云存储中，所以接下来，需要设置相应的“Cloud Storage Container”和username，即云存储地址和用户口令。注：购买Oracle云后，系统会提供对应的云存储地址和用户口令信息。
第2部分勾选“Create Cloud Storage Container”，即系统自动在云存储中，创建相应的存储容器。

![**<图片9>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/provisioning/9.jpg)

配置信息汇总，确认无误后，点击创建服务：

![**<图片10>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/provisioning/10.jpg)

开始创建实例，在MySQL云服务首页可以看到实例正在创建中，

![**<图片11>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/provisioning/11.jpg)


创建成功，整个创建过程只用了短短的10分钟。

















