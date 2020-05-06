<h2>fork from https://github.com/a970066364/spring-cloud-alibaba-seata/（nacos文档实在是太烂了，感谢这位前辈自己整理了demo）</h2>

----------------------

几点说明：

1、core-service/seata-server/conf/ 目录，是seata-server 1.1.0 conf目录，直接覆盖，并执行sql
----------------------
  
    # 下面seata-server/conf/registry.conf
    
    config {
      # file、nacos 、apollo、zk、consul、etcd3
      type = "nacos"
    
      nacos {
        serverAddr = "localhost:8848"
        group = "SEATA_CONFIG_GROUP"
        namespace = ""
        cluster = "default"
      }
    }
    
  - SEATA_CONFIG_GROUP 对应到各个服务下的registry.conf配置

2、把core-service/application.properties 配置导入nacos（执行HttpPostUtils.main）
----------------------

    service.vgroupMapping.myTestTxGroup=default
    
  - myTestTxGroup 对应到各个服务下application.properties 
  
    
    spring.cloud.alibaba.seata.tx-service-group=myTestTxGroup
    
3、执行各服务下的sql创建业务库
----------------------

4、发起请求，模拟用户下单：POST 127.0.0.1:15020/api/v1/order/generate
----------------------
