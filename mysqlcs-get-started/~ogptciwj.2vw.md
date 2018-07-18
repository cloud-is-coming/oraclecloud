# Oracle MySQL云服务入门系列5：MySQL企业监控	


接上文：

[Oracle MySQL云服务入门系列1：创建MySQL实例](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/mysqlcs-get-started-series1_provisioning.md)

[Oracle MySQL云服务入门系列2：访问MySQL实例](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/mysqlcs-get-started-series1_access.md)

[Oracle MySQL云服务入门系列3：MySQL实例生命周期管理](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/mysqlcs-get-started-series3_lifecycle.md)

[Oracle MySQL云服务入门系列4：MySQL自动备份和恢复](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/mysqlcs-get-started-series4_backup.md)

本文为Oracle MySQL云服务入门系列第五篇：MySQL企业监控。

本文我们将演示通过图形化的Web控制台，对MySQL实例进行实施监控，整个过程不需要安装代理，也不需要做任何配置。



**查看MySQL实例性能概要信息**

当有用户反馈应用的性能出现问题时，怀疑是数据库出现性能瓶颈，这个时候，数据库管理员可以登录MySQL实例主界面，通过Web控制台来检查数据库实例的性能情况。

在MySQL实例主界面，点击右上角的心电图图标，获取实例当前的性能信息。


《图片1》

![**<图片1>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/1.jpg)

查看实例的性能概要信息，如图：

《图片2》
![**<图片2>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/2.jpg)


**使用加密隧道方式访问MySQL企业监控器**

上面的方法只能查看MySQL实例性能的概要信息，如果想精确的定位系统的性能瓶颈，我们还需要获得MySQL实例的运行的各种性能指标，在本地环境中，Oracle提供了企业监控器（Enterprise Monitor），可以全方位的获得MySQL的运行状态信息，方便运维人员分析性能瓶颈，并找到解决方法。

在MySQL云服务中，Oracle同样提供了企业管理器界面，帮助运维人员便利的监控和运行数据库实例。

在创建MySQL实例的过程中，如果我们设置了企业管理器（本例已经设置了企业管理器），那我们就能直接使用了。 需要说明一点， 在公有云环境中， 系统安全是第一考虑要素， 所以缺省情况下， 系统自动禁用了企业管理器的访问端口。

我们可以通过两种方式来访问企业监控器，第一种是通过SSH加密隧道的方式，在本地建立一个SSH加密通道， 把本地的18443端口通过加密通道映射到MySQL实例的18443端口，然后通过Web浏览器访问127.0.0.1:18443来使用云上的企业监控器。

使用Putty设置加密通道，与前面的文章（访问MySQL）中提到的，通过Putty连接MySQL实例类似，不同的地方在于，在设置Putty的步骤中需要增加一步，设置加密隧道（Tunnels），点击“Tunnels”，在右边的“Add new forwarded port”部分，进行以下设置：

**Source Port**：设置本地映射端口，输入18443；

**Destination**：设置目标，输入MySQL实例的IP地址和企业监控器的端口（18433）；

其他部分保留缺省设置（勾选**Local**和**Auto**）。

然后点击添加，在“Forwarded Ports”区域就能看到刚刚添加的记录（L18443）。 点击“Open”，建立一个Putty会话。

这样就已经把本地的18443端口通过SSH加密通道映射到MySQL实例的18443端口。我们就可以通过浏览器，访问本地（127.0.0.1）的18443端口，就能访问到MySQL云服务的企业监控器了。 **注意： 在访问企业监控器的过程中，一定要保持这个Putty会话的连接，一旦会话中断，也就意味着加密隧道中断，将无法访问企业监控器。**


《图片3》
![**<图片3>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/3.jpg)

使用浏览器访问企业监控器， 在地址栏中输入以下地址：
https://127.0.0.1:18443

系统会提示信息：“您的连接不是私密连接”，点击**“高级”**，然后点击**“继续前往127.0.0.1（不安全）”**。

《图片4》

![**<图片4>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/4.jpg)

进入MySQL 企业监控器（MySQL Enterprise Monitor）登录界面，输入用户名和口令，注：在创建MySQL实例时，我们已经设置了用户名和口令。

《图片5》
![**<图片5>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/5.jpg)

进入企业监控器主页，我们可以通过企业监控器查看MySQL实例的各种运行状态信息，使用方法与本地版完全一致，这也是采用Oracle MySQL云服务的一个好处，自带的企业管理器，无法任何配置和代理。

《图片6》
![**<图片6>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/6.jpg)

比如我们要查看前面步骤中的备份状态信息，点击左侧的“Backups”，就能看到所有备份的信息，如图：

《图片7》
![**<图片7>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/7.jpg)

点击最近一次备份，就能看到此次备份的详细信息。

《图片8》
![**<图片8>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/8.jpg)


**备注：从安全的角度考量，Oracle强烈建议用户，使用加密隧道的方式来访问云上的MySQL企业监控器。**




**直接访问MySQL企业监控器**


老余一直在强调：**“企业上云，安全压倒一切！”** 但是肯定会有人想偷懒，觉得用加密隧道的方式太麻烦，想通过直连的方式访问企业管理器。  通常情况下，对于这种需求，老余在内心里是拒绝的，不过，为了凑字数，我还是告诉你，其实方法还是有的，而且很简单。

前面我已经提到过，企业管理器已经跟实例一起配置好了，只是端口被系统缺省设置为禁用，无法直接访问。其实只需要管理员在访问规则（Access Rule）里启用即可。

在MySQL实例的主界面，点击右上角的下拉菜单，可以看到两个选项：“Enterprise Monitor URL”和“Access Rules”，我们可以通过点击“Enterprise Monitor URL”选项直接访问企业监控器，但是前提是，我已经在“Access Rules”里启用了企业监控器。 点击“Access Rules”选项，进入访问规则设置页面。

《图9》
![**<图片9>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/9.jpg)

可以看到，有一条访问规则ora_p2admin_em，它的状态是禁用的。这就是企业监控器的访问规则。点击该规则后面的下拉菜单，点击“Enable”。

《图10》
![**<图片10>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/10.jpg)

确认开启该访问规则，点击“Enable”

《图11》
![**<图片11>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/11.jpg)

访问规则设置完成，查看状态，已经为启用状态。

《图12》
![**<图片12>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/12.jpg)

返回到实例主界面，在右上角的下拉菜单中，点击“Enterprise Monitor URL”选项，就可以直接访问企业监控器了。

《图13》
![**<图片13>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/13.jpg)

《图14》
![**<图片14>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/monitor/14.jpg)

**至此，《MySQL云服务入门》系列文章已经完结，更多精彩等待大家去发掘！**
