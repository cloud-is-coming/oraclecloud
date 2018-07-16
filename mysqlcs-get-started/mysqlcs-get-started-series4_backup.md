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

前面我们已经演示了怎样备份和恢复一个MySQL实例，在DBA的日常工作中，除了在每次系统变更前，提前备份好数据库，并在数据库出现问题时，用备份来恢复数据库外。作为一个称职的DBA，更重要的工作是根据数据库的实际情况，制定合理的备份/恢复策略，同时尽量将这些备份/恢复策略做成定期自动执行的任务，并定期检查这些自动计划的执行情况，以确保备份/恢复策略的有效。

下面将介绍如何通过图形化界面来设置自动备份计划。
进入MySQL实例的“管理”界面，点击“Available Backups”右侧的下拉菜单，选择“Configure Backups”选项，进入备份设置界面：

《图片11》
![**<图片11>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/11.jpg)

在“Configure Backups”界面，根据数据库的实际情况设置以下策略：
Full Backup： 数据库全备时间，本例设置为每周一18点做一次全库备份；

Incremental Backup：数据库增量备份时间，本例为每天20点做一次数据库增量备份；

Retention Period： 数据库备份的保留时间，缺省为30天。


《图12》
![**<图片12>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/12.jpg)

自动备份计划设置完成后，我们可以在“管理”界面的“Backup”的概要页面上看到已经设置好的自动备份计划，如图：



《图13》
![**<图片13>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/13.jpg)

备注：
区域1 显示： 每天下午8点执行增量备份；
区域2 显示： 每天下午6点执行全库备份；
区域3 显示： 最近一次成功备份的时间。


**数据库备份保留策略**

随着时间的推移，数据库的备份会越来越多，会影响日常数据库备份的管理，同时也会消耗过多的存储空间，因此需要设置比较合理的数据库备份保留策略。

数据库备份的清理方式跟数据库的备份方式相关。
我们在前面已经提到过，数据库备份方式有两种，一种是设置自动备份计划，由系统定时自动执行备份任务，在设置备份计划时，会要求同时设置备份的保留时间，例如本文就是按照缺省设置，备份的保留时间是30天，即系统会自动清除超过30天以上的备份，而且这类备份是无法通过人工方式直接清除，如果确实需要提前清除此类备份，我们可以通过修改备份计划中的“备份保留时间”的方式来清理。 

我们可以看到该实例所有成功的备份，每次备份的“Notes”明确的表明此次是通过自动备份计划发起的，还是手工发起的。

“Notes”描述为“自动备份”，说明是自动备份计划发起的，我们不能直接删除此类备份，只能通过修改备份保留时间的方式来清除。

《图14》
![**<图片14>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/14.jpg)

第二种备份是由管理员通过Web管理界面，手工发起的备份，对于此类备份，我们可以在图形化界面中，直接删除，如图：

《图15》
![**<图片15>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/15.jpg)

确认删除备份。

《图16》
![**<图片16>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/backup/16.jpg)


