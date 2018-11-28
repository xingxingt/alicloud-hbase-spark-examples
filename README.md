### Spark分析HBase数据有“RDD API”、“SQL API”、“HFILE”三种方式，相关对比如下：

![](https://ws2.sinaimg.cn/large/006tNbRwly1fxnja3po27j30u00xs0w8.jpg)

对于数据动态更新增加的小表推荐使用SQL API的方式，可以有效的优化分析，减少对HBase集群稳定性的影响；对于静态表或者全量静态表的分析推荐使用分析HFILE的方式直读HDFS，这样可以完全不影响HBase集群稳定性；不推荐使用RDD API 的方式，这种方式一方没有优化性能差，同时在高并发以及表数据量大时，会严重影响HBase集群的稳定性，从而影响在线业务。




### alicloud-hbase-spark-examples
1、在examples/conf/hbase-site.xml中配置alihbase的zkurl

2、下载alihbase以及aliphoenix的客户端，里面包含spark分析hbase数据时需要的jar包

3、eg：

a、spark-submit  --class org.apache.spark.hbase.NativeRDDAnalyze --master yarn-client --jars shc-core-1.1.0-2.1-s_2.11.jar,/home/hadoop/muyuan/alihbase-1.1.1/lib/alihbase-common-1.1.1.jar,/home/hadoop/muyuan/alihbase-1.1.1/lib/alihbase-server-1.1.1.jar,/home/hadoop/muyuan/alihbase-1.1.1/lib/alihbase-client-1.1.1.jar,/home/hadoop/muyuan/alihbase-1.1.1/lib/alihbase-protocol-1.1.1.jar  shc-examples-1.1.0-2.1-s_2.11.jar 

b、spark-submit  --class org.apache.spark.sql.execution.datasources.hbase.SqlAnalyze --master yarn-client --jars shc-core-1.1.0-2.1-s_2.11.jar,/home/hadoop/muyuan/alihbase-1.1.1/lib/alihbase-common-1.1.1.jar,/home/hadoop/muyuan/alihbase-1.1.1/lib/alihbase-server-1.1.1.jar,/home/hadoop/muyuan/alihbase-1.1.1/lib/alihbase-client-1.1.1.jar,/home/hadoop/muyuan/alihbase-1.1.1/lib/alihbase-protocol-1.1.1.jar   shc-examples-1.1.0-2.1-s_2.11.jar 

c、spark-submit  --class org.apache.spark.phoenix.connector.PhoenixTest --master yarn-client --jars shc-core-1.1.0-2.1-s_2.11.jar,/home/hadoop/muyuan/alihbase-1.1.1/lib/alihbase-common-1.1.1.jar,/home/hadoop/muyuan/alihbase-1.1.1/lib/alihbase-server-1.1.1.jar,/home/hadoop/muyuan/alihbase-1.1.1/lib/alihbase-client-1.1.1.jar,/home/hadoop/muyuan/alihbase-1.1.1/lib/alihbase-protocol-1.1.1.jar,/home/hadoop/muyuan/phoenix-4.11.0-AliHBase-1.1-0.3/phoenix-4.11.0-AliHBase-1.1-0.3-server.jar,/home/hadoop/muyuan/phoenix-4.11.0-AliHBase-1.1-0.3/phoenix-spark-4.11.0-HBase-1.1.jar   shc-examples-1.1.0-2.1-s_2.11.jar 
