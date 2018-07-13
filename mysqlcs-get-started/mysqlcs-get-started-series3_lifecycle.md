# Oracle MySQL云服务入门系列3：MySQL实例生命周期管理


接上文：

[Oracle MySQL云服务入门系列1：创建MySQL实例](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/mysqlcs-get-started-series1_provisioning.md)

[Oracle MySQL云服务入门系列2：访问MySQL实例](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/mysqlcs-get-started-series1_access.md)





本文为Oracle MySQL云服务入门系列第三篇：MySQL实例生命周期管理。

在前面的文章中，我们已经介绍如何在Oracle云上创建一个MySQL实例，另外演示如何访问MySQL实例，同时设置允许应用服务器访问数据库实例。

MySQL云服务提供了多种手段来管理MySQL实例，比如REST API接口，命令行工具，以及图形化的Web控制台。本文我们将演示通过图形化的Web控制台，对MySQL实例进行生命周期管理。



**通过浏览器登录Oracle云主页**

在浏览器登录到MySQL云服务的主页：

《图片1》
![**<图片1>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/1.jpg)



点击实例名"DemoDB",进入该实例的主界面：

《图片2》
![**<图片2>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/2.jpg)


点击Resouce区域的下拉菜单按钮，下拉菜单中有3个选项：重新启动、纵向扩展和Add Storage。我们通过这些选项，来实现重启实例、为实例新增CPU和内存和新增存储空间等功能。如图：


《图片3》
![**<图片3>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/3.jpg)

另外，我们也可以点击右上角的下拉菜单，来设置MySQL实例，如图：

《图片4》
![**<图片4>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/4.jpg)

**启停MySQL实例**


点击“停止”按钮关闭MySQL实例，在弹出窗口中，点击确认，如图：

《图片5》
![**<图片5>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/5.jpg)

**实例正在停止中**

《图片6》
![**<图片6>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/6.jpg)

实例已经停止完毕。

**启动实例。**

《图片7》
![**<图片7>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/7.jpg)

**实例启动中**

《图片8》
![**<图片8>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/8.jpg)

**通过图形界面来纵向扩展MySQL实例**

随着业务的增长，MySQL实例的系统资源可能无法满足需求，需要通过增加CPU和内存来增加事务处理能力。在MySQL云服务中，我们可以在图形化界面上，通过简单的点击操作，就能轻松的实现MySQL实例的纵向扩展。

进入实例主界面，当前的配置为1 OCPU/ 7.5 GB 内存/ 175 GB存储。我们希望通过Web Console界面，为实例增加7.5 GB 内存。

点击Resouce区域的下拉菜单，选择“纵向扩展服务”，如图：

《图片9》
![**<图片9>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/9.jpg)

在“MySQL Server计算配置”下拉框中选择需要增加的系统资源，选择“OC1m-1.0 OCPU, 15.0GB RAM”，点击“是，纵向扩展服务”。
**注：新增系统资源需要重启实例，所以，纵向扩展操作期间服务将不可用。在生产环境中做次操作前，需要提前申请停机窗口**

《图片10》
![**<图片10>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/10.jpg)

实例处于纵向扩展状态，服务不可用。

《图片11》
![**<图片11>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/11.jpg)

内存添加成功，现在实例的配置为1 OCPU/ 15 GB 内存/ 175 GB存储。

《图片12》
![**<图片12>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/12.jpg)


**通过图形界面来为MySQL实例增加存储空间**

前面我们已经成功的为MySQL实例新增加了7.5GB的内存，现在我们将演示为数据库增加25GB的“可用数据库存储”。

当前，实例共使用175GB的存储空间，其中数据库的可用空间为25GB,我们可以通过点击“Add Storage”来增加“可用数据库存储”。

《图片13》
![**<图片13>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/13.jpg)

在Add Storage界面，将“可用数据库存储”从25 GB修改为50 GB，即新增25 GB的可用数据库存储。
**注：新增系统资源需要重启实例，所以，纵向扩展操作期间服务将不可用。在生产环境中做次操作前，需要提前申请停机窗口**

《图片14》
![**<图片14>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/14.jpg)

实例处于“Adding Storage”状态，服务不可用。

《图片15》
![**<图片15>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/15.jpg)

数据库存储添加成功，现在实例的配置为1 OCPU/ 15 GB 内存/ 200 GB存储。

《图片16》
![**<图片16>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/lifecycle/16.jpg)








