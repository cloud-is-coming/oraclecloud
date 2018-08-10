## Oracle自治事务处理云服务抢先体验3--向ATP数据库中加载数据


#[Loading Your Data to Autonomous Transaction Processing](http://www.oracle.com/webfolder/technetwork/tutorials/obe/cloud/atp/OBE_Loading%20Your%20Data%20Into%20Autonomous%20Transaction%20Processing/loading_your_data_Into_autonomous_transaction_processing.html)  

将数据加载到ATP中
本文将介绍如何将云存储中的数据加载到ATP数据库中。
有多种方法来实现ATP数据库的数据加载，可以用Oracle数据库自带工具、采用Oracle或第三方的数据集成工具。另外，可以将本地客户端上的文件加载到ATP中，也可以将云对象存储中的文件加载进去。

Oracle推荐使用方法：先将数据上传到云存储上，再从云存储中加载到ATP中，这是加载速度最快的方式。数据加载需要用到ATP数据库中的一个新引入的包DBMS_CLOUD。DBMS_CLOUD目前支持Oracle Cloud Infrastructure Object Storage, Oracle Cloud Infrastructure Object Storage Classic, and Amazon AWS S3。

本次实验，我们将演示以下步骤：先将数据文件上传OCI Object Storage上，然后从OCI Object Storage把数据加载到ATP中。整个过程需要用到DBMS_CLOUD包里的两个存储过程：create_credential 和 copy_data，其中create_credential是用来把对象存储的认证令牌存放到ATP的Schema中，copy_data是用来将数据从文件中加载到数据表中。

《图1》
![**<图片1>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/1.png)



《图2》
![**<图片2>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/2.png)



《图3》
![**<图片3>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/3.png)



《图4》
![**<图片4>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/4.png)


《图5》
![**<图片5>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/5.png)


《图6》
![**<图片6>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/6.png)




《图7》
![**<图片7>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/7.png)


《图8》
![**<图片8>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/8.png)


《图9》
![**<图片9>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/9.png)


《图10》
![**<图片10>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/10.png)




《图11》
![**<图片11>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/11.png)



# Create an Object Store Auth Token
创建对象存储认证令牌
To load data from an Oracle Cloud Infrastructure Object Storage object store, you need to create an Auth Token for your object store account. The communication between your Autonomous Transaction Processing database and the object store relies on the Auth Token and username/password authentication.


《图12》
![**<图片12>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/12.png)

《图13》
![**<图片13>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/13.png)

《图14》
![**<图片14>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/14.png)


《图15》
![**<图片15>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/15.png)

《图16》
![**<图片16>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/16.png)

《图17》
![**<图片17>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/17.png)






Token：r9aionww6H_-Gki);qmJ


**创建好Authority Token**

《图18》
![**<图片18>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/18.png)






#Create Object Store Credentials in your Autonomous Transaction Processing Schema
Now that you have created an object store Auth Token, store in your Autonomous Transaction Processing atpc_user schema the credentials of the object store in which your data is staged.

《图19》
![**<图片19>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/19.png)



begin
  DBMS_CLOUD.create_credential (
credential_name => 'OBJ_STORE_CRED',
username => '13#######@139.com',
password => 'r9aionww6H_-Gki);qmJ'
  ) ;
end;
/


脚本执行成功后，我们已经将对象存储的令牌文件（Auth Token）存储到ATP的schema atpc_user中。


**将云对象存储中的文件数据加载到ATP的表中。**




格式如下：
https://objectstorage. <region name>.oraclecloud.com/n/<tenant name>/b/tutorial_load_atpc/o/chan_v3.dat
https://swiftobjectstorage.<region name>.oraclecloud.com/v1/<tenant name>/tutorial_load_atpc/chan_v3.dat
注意：其中<region name>用区域名称代替，如us-ashburn-1，<tenant name>用租户名代替，即云账号名。

《图20》
![**<图片20>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/20.png)




查看数据是否加载

《图21》
![**<图片21>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/21.png)





执行SQL语句，根据输出结果检查数据是否加载成功。


	SELECT table_name, owner_name, type, status, start_time, update_time, 
	logfile_table, badfile_table 
	FROM user_load_operations WHERE type = 'COPY';
	

《图22》
![**<图片22>**](https://github.com/cloud-is-coming/oraclecloud/blob/master/atp-get-started/Loading/22.png)









