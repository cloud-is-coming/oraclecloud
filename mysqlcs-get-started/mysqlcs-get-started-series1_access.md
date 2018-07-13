# Oracle MySQL云服务入门系列2：访问MySQL实例


接上文：[Oracle MySQL云服务入门系列1：创建MySQL实例](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/mysqlcs-get-started-series1_provisioning.md)



本文为Oracle MySQL云服务入门系列第二篇：访问MySQL实例。在上一篇文章中，我们已经在Oracle云上，通过图形界面快速创建一个MySQL实例。现在我们需要连上MySQL实例，创建相关的数据库对象，同时我们的应用也需要访问数据库。本文我们将演示如何访问MySQL实例，同时设置允许应用服务器访问数据库实例。



**通过浏览器登录Oracle云主页**

在浏览器登录到MySQL云服务的主页：

![**<图片1>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/1.jpg)


点击实例名"DemoDB",进入该实例的主界面：

![**<图片2>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/2.jpg)


找到实例的公共IP地址，我们需要通过IP地址和端口号来访问数据库实例。



**通过Putty访问MySQL实例**

与其他云厂商不同，MySQL云服务中创建好的MySQL实例对外已经提供了访问端口，缺省3306（可自行修改），应用程序或开发工具可以通过该端口访问MySQL数据库，用户只需要使用MySQL服务，而无需管理服务的基础设施，这也是PaaS服务相比于IaaS服务的最大特点：用户只需要关注服务本身，底层的基础设施完全交给云服务商。即便如此，Oracle还是很人性化的为用户提供了另一个选择：用户可以拥有实例操作系统的root权限，对根据需要，执行操作系统级的操作。为了安全考虑，用户只能使用SSH 密钥对的方式，通过22端口访问实例的操作系统。
下面来演示使用Putty工具，通过SSH密钥的方式来访问MySQL实例的操作系统。

打开Putty，在Connection区域点击“SSH”下的“Auth”，在右侧的Private Key file部分选择密钥文件：

![**<图片3>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/3.jpg)


点击"Session"，在Host Name处输入MySQL实例的公共IP地址，端口缺省22，点击打开：


![**<图片4>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/4.jpg)

注：在第一篇文章中，在创建MySQL实例时，有一步需要提供公钥，目的就是为了让用户通过SSH密钥对的方式访问操作系统。如何创建密钥对，可以参加文章[《配置SSH通过密钥访问Ravello中的服务》](https://mp.weixin.qq.com/s?__biz=MzIzNjg2NjY1MQ==&mid=2247485612&idx=1&sn=eff53e42991dead4eeafe2a3a5f4ae3e&chksm=e8d01598dfa79c8ed056706de8f78a6331a946e2f5c1d39c8d92f3a63fa78c7f8e3512a08449#rd)。


输入用户名 opc，进入操作系统界面，系统自动显示MySQL实例的详细信息：


![**<图片5>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/5.jpg)

使用sudo切换到oracle用户，运行MySQL客户端：
$ sudo su - oracle
$ mysql


![**<图片6>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/6.jpg)

查看所有数据库信息：
mysql> show databases;


![**<图片7>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/7.jpg)

现在我们可以通过MySQL客户端，直接创建数据库对象。
另外，MySQL云服务也支持各种标准的MySQL驱动。接下来，我们将演示如何设置访问规则，确保应用服务器可以通过标准的MySQL驱动来访问MySQL实例。
为了安全考虑，缺省情况下，MySQL云服务禁止外部访问请求。必须设置访问规则，才能确保应用服务器正常访问数据库服务。

**配置应用服务器访问MySQL实例**

在DemoDB实例的主界面，点击右侧的下拉菜单按钮，点击“Access Rules”，进入访问规则设置界面，如图：


![**<图片8>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/8.jpg)

点击“Create Rule”按钮，创建新的访问规则：


![**<图片9>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/9.jpg)

输入访问规则相关配置信息：

**Rule Name**：app-server-access

**Source**：选择<custom>，自定义访问源，在下面的文本框中输入应用服务器的IP地址或者网段，允许这些服务器或者网段访问MySQL服务。注：如果是多个IP地址，必须用逗号分开，如果是网段，必须是CIDR格式。

**Destination**：选择mysql_MASTER,即可以访问MySQL实例。注：另一个选项是mysql_ADMIN_HOST,即允许访问操作系统。

**Destination Port(s)**: 输入3306，即允许应用服务器通过3306端口访问MySQL实例。注：端口可以自定义，但必须与MySQL实例开放的端口一致。

**Protocal**：选择TCP协议。

配置完成，点击Create。

![**<图片10>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/10.jpg)

访问规则创建成功，现在指定的应用服务器就可以通过3306端口，直接访问MySQL实例了。


![**<图片11>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/mysqlcs-get-started/access/11.jpg)



















