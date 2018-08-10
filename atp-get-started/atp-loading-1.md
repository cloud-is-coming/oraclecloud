# Oracle自治事务处理云服务抢先体验1--创建ATP实例



2018年8月7日，Oracle执行董事长兼首席技术官拉里·埃里森发布了一款新服务：Oracle自治事务处理云服务（Autonomous Transaction Processing，简称ATP）。 这是Oracle公司“自治云平台”战略的一个重要里程碑。利用创新的机器学习和自动化功能，Oracle Autonomous Transaction Processing提供了前所未有的成本节约、安全性、可用性和生产力。Oracle新的自治数据库云服务是为了运行世界上最苛刻的金融、零售、制造和政府应用程序，支持高性能事务处理、报告、批处理和分析工作负载的复杂组合。Oracle的自主数据库组合为组织提供了当今市场上最完整和最先进的数据库功能集。


原文参见链接：[Larry Ellison Announces Availability of Oracle Autonomous Transaction Processing](https://www.oracle.com/corporate/pressrelease/oracle-autonomous-transaction-processing-080718.html). 


有关“Oracle自治数据库”的新闻铺天盖地，非常吸引眼球。这段时间陆续有一些正式发布，如ADW(Autonomous Data Warehouse，简称ADW)服务，而深受广大DBA同学关注的自治OLTP服务，今天终于解开了神秘的面纱，请记住她的名字：Oracle自治事务处理云服务（Autonomous Transaction Processing，简称ATP）。
更多的官方介绍，请移步：[ATP官网介绍](https://cloud.oracle.com/zh_CN/atp)。


作为一个技术小白，俺们对官方广告不感兴趣，就想上手试一把。
手上的资料不多，不能太深入，就从创建实例、连接实例下手。

##创建ATP实例

进入Oracle云的Web控制台，选择进入OCI服务，提前说明，ATP刚刚发布，目前只部署在少数几个区域，如：
Region Location	Region Name	Region Key

Ashburn, VA	us-ashburn-1	IAD

Frankfurt, Germany	eu-frankfurt-1	FRA

Phoenix, AZ	us-phoenix-1	PHX

所以只能在以上几个区域中创建。

很巧，我手上的账号位于区域us-ashburn-1，正好可以体验ATP。

点击左上角的“MENU”下拉菜单，在菜单中选择“Autonomous Transaction Processing”选项。

《图1》
![**<图片1>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/provisioning/1.png)

在创建ATP实例前，先要创建一个COMPARTMENT，一个新账号会缺省创建2个COMPARTMENT，这都是给系统自用的，有点像system表空间一样，强烈建议新创建一个COMPARTMENT来存放各种新建的服务。 在我的账号中刚好已经创建了一个名为YC-TEST的COMPARTMENT，所以我们可以从左侧的COMPARTMENT下拉框中选择YC-TEST，然后点击按钮“Create Autonomous Transation Processing”，开始创建ATP实例。

《图2》
![**<图片2>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/provisioning/2.png)

自治服务的优势有很多，其中的一个特点就是：创建服务的过程非常简易。 只需要少数配置，就可以快速创建一个ATP服务。

下面就是ATP实例的配置界面，来看看需要配置哪些参数：

《图3》
![**<图片3>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/provisioning/3.png)

**Display Name**：设置实例的名称。

**Database Name**： 设置数据库名称，要求只能包含数字和字母，不超过14个字符。

**CPU Core Count**:  设置数据库使用的CPU核数，一个数据库最多可以使用128核CPU。

**Storage**: 设置数据库的存储空间，一个数据库最多可以使用128TB的数据库空间。

**Administrator Credentials**： 设置数据库管理员口令，管理员名称为ADMIN，为缺省设置，不能修改，按照要求设置管理员口令。

**License**： 设置授权模式，可以使用BYOL，可以选择订阅新的数据库软件license和数据库云服务，本例中采用BYOL。

设置以上参数后，就可以点击确认按钮，开始创建ATP实例。 等等，怎么这么快就开始创建了， 建一个数据库不是要设置很多参数吗？像SGA、PGA、字符集等都是必须手工设置的，另外还有一些关键的初始化参数也是要调整的，而且等数据库建好后， 可能还要根据数据库的使用情况适当的调整一些参数。这些参数在哪设置？
答案是：不需要！！！  这些设置都由系统自动调整，根本不需要人干预，不然怎么叫自治数据库呢？


- **自治驾驶**：实现所有管理，监控，调优自动化。 

- **自治安全**：防止外部攻击和恶意内部用户。 

- **自治修复**：防止包括计划维护在内的所有停机时间。


据说以上自治能力均由内置机器学习能力实现！ 很炫酷吧！

点完确定按钮后，开始创建ATP实例。

《图4》
![**<图片4>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/provisioning/4.png)

几分钟后，ATP实例创建成功！下面是创建好的ATP实例界面，我们可以点击“Service Console”界面进入ATP数据库的控制台，第一时间感受一下ATP。

《图5》
![**<图片5>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/provisioning/5.png)

需要数据管理员口令，管理员的用户名是ADMIN（这是缺省设置的），口令是前面我们自己设置的。

《图6》
![**<图片6>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/provisioning/6.png)

查看ATP实例的概率：存储空间使用情况、CPU的使用情况、SQL的运行情况等。

《图7》
![**<图片7>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/provisioning/7.png)

点击“Activity”，查看ATP数据库的主要运行指标，如数据库的活动数、CPU利用率等。

《图8》
![**<图片8>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/provisioning/8.png)

点击“Adminitration”，可以做一些管理工作，如：下载客户端信任文件、设置管理员口令等。其中下载客户端信任文件的工作很重要，因为客户端连接ATP数据库时，必须采用这个客户端信任文件。

《图9》
![**<图片9>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/provisioning/9.png)

点击“Download Client Credentials”，下载客户端信任文件。

《图10》
![**<图片10>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/provisioning/10.png)

输入管理员口令，点击“Download”下载。系统会生成一个wallet zip文件，把这个文件存放一个目录下。注意：一定好妥善保管好这个文件，客户端连接ATP实例时，必须要使用这个文件，如果被其他非授权用户拿到，就会存在数据库安全风险。

《图11》
![**<图片11>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/provisioning/11.png)




