# Oracle MySQL云服务入门系列4：MySQL自动备份和恢复	


接上文：

[Oracle MySQL云服务入门系列1：创建MySQL实例](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/mysqlcs-get-started-series1_provisioning.md)

[Oracle MySQL云服务入门系列2：访问MySQL实例](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/mysqlcs-get-started-series1_access.md)

[Oracle MySQL云服务入门系列3：MySQL实例生命周期管理](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/mysqlcs-get-started-series3_lifecycle.md)



本文为Oracle MySQL云服务入门系列第四篇：MySQL自动备份和恢复。

本文我们将演示通过图形化的Web控制台，对MySQL实例进行单次备份和恢复，并设置一个自动备份计划。



**通过浏览器登录MySQL备份恢复界面**

在MySQL实例主界面，点击“管理”区域

《图片1》
![**<图片1>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/1.jpg)

**备份MySQL实例**

点击"Available Backups"区域旁的下拉菜单，选择“Backup Now”。

《图片2》
![**<图片2>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/2.jpg)

为本次备份添加备注后， 点击“Back Up”按钮，开始备份。

《图片3》
![**<图片3>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/3.jpg)

备份开始。

《图片4》
![**<图片4>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/4.jpg)

点击钟表图标，查看备份信息：

《图片5》
![**<图片5>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/5.jpg)


备份成功，点击钟表图标，查看备份信息：

《图片6》
![**<图片6>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/6.jpg)


**恢复MySQL实例**

当数据库发生故障，如数据文件损坏等，需要使用备份来进行恢复。
进入"Available Backups"区域，选择最近一次成功的备份，点击右边的下拉菜单，选择“Restore”选项：

《图片7》
![**<图片7>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/7.jpg)


为本次恢复添加备注后， 点击“Restore”按钮。

《图片8》
![**<图片8>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/8.jpg)

再次确认，点击“Yes, Restore Instance”，正式开始使用备份来恢复数据库。

《图片9》
![**<图片9>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/9.jpg)

实例恢复中。

《图片10》
![**<图片10>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/10.jpg)



**设置自动备份计划**



