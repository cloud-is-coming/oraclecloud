## Oracle自治事务处理云服务抢先体验3--向ATP数据库中加载数据


Oracle自治事务处理云服务抢先体验系列：

[Oracle自治事务处理云服务抢先体验1：创建ATP实例](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/atp-provisioning-1.md)

[Oracle自治事务处理云服务抢先体验2：连接ATP实例](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/atp-connecting-1.md)

[Oracle自治事务处理云服务抢先体验3：向ATP数据库中加载数据](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/atp-loading-1.md)

 

###**将数据加载到ATP中**
本文将介绍如何将云存储中的数据加载到ATP数据库中。
有多种方法来实现ATP数据库的数据加载，可以用Oracle数据库自带工具、采用Oracle或第三方的数据集成工具。另外，可以将本地客户端上的文件加载到ATP中，也可以将云对象存储中的文件加载进去。

Oracle推荐使用方法：先将数据上传到云存储上，再从云存储中加载到ATP中，这是加载速度最快的方式。数据加载需要用到ATP数据库中的一个新引入的包DBMS_CLOUD。

DBMS_CLOUD目前支持Oracle Cloud Infrastructure Object Storage, Oracle Cloud Infrastructure Object Storage Classic, and Amazon AWS S3。

本次实验，我们将演示以下步骤：先将数据文件上传OCI Object Storage上，然后从OCI Object Storage把数据加载到ATP中。整个过程需要用到DBMS_CLOUD包里的两个存储过程：create_credential 和 copy_data，其中create_credential是用来把对象存储的认证令牌存放到ATP的Schema中，copy_data是用来将数据从文件中加载到数据表中。

我们先把本文实验需要用到的数据文件下载下来，[下载SH表数据文件](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/scripts/datafiles_for_SH_tables.zip)。

将数据文件压缩包下载到本地文件夹中，并解压缩。

###**将数据文件上传到OCI对象存储中**

进入OCI主界面，点击左上角“MENU”下拉菜单，选择“Object Storage”-“Object Storage”，如图：

《图1》

![**<图片1>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/1.png)


输入租户名：

《图2》
![**<图片2>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/2.png)


选择Single Sign On 登录：

《图3》
![**<图片3>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/3.png)


进入对象存储主界面后，点击“Create Bucket”创建一个Object Storage Bucket。注意：在左边的COMPARTMENT下拉菜单中，选择新建的COMPARTMENT（非系统自带），如本例中的YC-TEST。

《图4》
![**<图片4>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/4.png)

输入Bucket名称，Object Storage Bucket类似于一个在对象存储中创建了一个目录，后面的步骤中，会将本地的数据文件上传到这个bucket中，我们可以以Bucket为单位对其他用户进行访问控制。

《图5》
![**<图片5>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/5.png)

查看已创建好的Bucket，主要该Bucket的“Storage Tier”为Standard，即标注的对象存储，另外一个选项是归档对象存储。 点击“Upload Object”按钮，准备将本地的数据文件上传到该Bucket。如图：

《图6》
![**<图片6>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/6.png)


在上传界面，选择上传文件所在本地位置。如图：

《图7》
![**<图片7>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/7.png)

查看本地的数据文件，如图：
《图8》
![**<图片8>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/8.png)

在上传界面中，将本地的数据文件一个个上传上去。注意：目前一次只能上传，不知道什么时候能批量上传。

《图9》
![**<图片9>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/9.png)

选中数据文件后，点击“Upload Object”，开始上传。
《图10》
![**<图片10>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/10.png)


依次将所有数据文件上传到bucket中，查看所有的文件是否上传完毕，如图。

《图11》
![**<图片11>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/11.png)



###创建对象存储认证令牌
在从OCI对象存储中加载数据前，需要先创建一个认证令牌（Auth Token）。ATP数据库与对象存储之间的通信，依赖于这个认证令牌和用户口令认证。


在OCI首页，点击“MENU”下拉菜单，选择“Identity”-“User”，进入User主界面，如图：

《图12》
![**<图片12>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/12.png)

在User主界面中，选择用户，进入该用户的主界面，如图：

《图13》
![**<图片13>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/13.png)


点击左侧"Resource"区域中的“Auth Tokens”，如图：

《图14》
![**<图片14>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/14.png)

点击“Generate Token”生成认证令牌（Auth Token）。
《图15》
![**<图片15>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/15.png)

给认证令牌加个描述。

《图16》
![**<图片16>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/16.png)


生成的认证令牌就是一段字符串，把它拷贝下来，妥善保管，后面的步骤需要用到它。

《图17》

![**<图片17>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/17.png)



本例中生成的认证令牌如下：

	
	Token：r9aionww6H_-Gki);qmJ



已经创建的认证令牌：

《图18》

![**<图片18>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/18.png)




###使用DBMS_CLOUD加载数据

在下面的步骤中，我们将在SQL Developer工具中，使用DBMS_CLOUD的两个过程，将上传到OCI对象存储中的数据文件加载到ATP数据库的 atpc_user schema下。

第一步，使用刚刚已经创建的认证令牌，在atpc_user schema中创建一个信任文件。这个过程要用到DBMS_CLOUD下的过程create_credential。

代码示例如下：


	begin
	  DBMS_CLOUD.create_credential (
	credential_name => 'OBJ_STORE_CRED',
	username => '13#######@139.com',
	password => 'r9aionww6H_-Gki);qmJ'
	  ) ;
	end;
	/

**注：**
username为OCI对象存储所属用户名。

password为刚刚生成的认证令牌。


将上面的SQL脚本在SQL Developer的工作表中执行
《图19》

![**<图片19>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/19.png)


脚本执行成功后，我们已经将对象存储的令牌文件（Auth Token）存储到ATP的schema atpc_user中。


第二步，使用DBMS_CLOUD包中的过程copy_data，最终将对象存储中的数据加载到atpc_user下相关数据表中。

先下载脚本模板，下载链接：[data_load脚本模板](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/scripts/data%20loading%20script.txt)

然后将脚本模板按照下面的说明进行修改。

	begin
	 dbms_cloud.copy_data(
	table_name =>'CHANNELS',
	credential_name =>'OBJ_STORE_CRED',
	file_uri_list =>'https://swiftobjectstorage.<tenant name>.oraclecloud.com/v1/<tenant name>/tutorial_load_atpc/chan_v3.dat',
	format => json_object('ignoremissingcolumns' value 'true', 'removequotes' value 'true')
	 );
	end;
	/


	这里需要修改file_uri_list内容，用正式的环境信息替代：

	https://swiftobjectstorage.<region name>.oraclecloud.com/v1/<tenant name>/tutorial_load_atpc/chan_v3.dat
	注意：其中<region name>用区域名称代替，如us-ashburn-1，<tenant name>用租户名代替，即云账号名。

数据加载脚本修改完毕，拷贝到SQL Developer的工作表中执行，如图：

《图20》

![**<图片20>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/20.png)




查看数据是否加载

《图21》

![**<图片21>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/21.png)




也可以通过执行SQL语句，根据输出结果检查数据是否加载成功。


	SELECT table_name, owner_name, type, status, start_time, update_time, 
	logfile_table, badfile_table 
	FROM user_load_operations WHERE type = 'COPY';
	

《图22》

![**<图片22>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/22.png)









