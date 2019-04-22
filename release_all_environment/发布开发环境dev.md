# 发布开发环境(dev)

开发环境(dev)
1. 所有开发项目都在几台较小配置服务器上运行，
不能确保每个项目组都能分配到固定的服务器，因此开发过程使用时，
则是见哪台服务器有空缺有资源，便可以部署项目。
2. 开发环境未采用config配置中心，因此配置走本地。
**注意事项：dev开发时，请检查`application.yml`中环境是否指定`dev`**

目前部署应用服务的服务器清单。

IP|	OS|	root密码|	port|	操作账号|	操作密码|作用
---|---|---|---|---|---|---
192.168.200.126|	centos7.5|	-|	22|	    arch-uoko|	archUoko@123|X端开发占用中
192.168.200.44|  	centos7.5|        -|	 22|	arch-uoko|	archUoko@123|基础组件占用中
192.168.200.45|  	centos7.5|        -|	 22|	arch-uoko|	archUoko@123|可部署其他服务
192.168.200.46|  	centos7.5|        -|	 22|	arch-uoko|	archUoko@123|可部署其他开发服务

* 配置信息检查
   
    * bootstrap.xml配置
      
      bootstrap.xml中的配置，在生成代码过程中是默认开启。因此需要开发人员自行修改。
      需将config关闭， `spring.cloud.config.enabled: false`。
      (**片外:如不修改本地会每5s请求`http://localhost:8888`类似的字样**)
      
      修改后的配置如下。
      
      ```
       spring:
             cloud:
               config:
                 uri: http://192.168.200.26:8040
                 name: uoko-platform-auth,uoko-system-common
                 profile: pro
                 label: master
                 enabled: false

      ```
    
    * consul配置检查
    
        ```
          cloud:
        #    service-registry:
        #      auto-registration:
        #        enabled: false
            consul:
              host: 192.168.200.22
              port: 8500
              discovery:
                healthCheckPath: /actuator/health
                healthCheckInterval: 5s
                enabled: true
                prefer-ip-address: true
              enabled: true
        ```
    * 其他额外参数检查
    
        * mysql 
          
          mysql 需连接到 
          ```
           spring:
              datasource:
                 url: jdbc:mysql://192.168.200.60:3336/uoko-platform-uc?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&useAffectedRows=true&zeroDateTimeBehavior=convertToNull&allowMultiQueries=true
                 driver-class-name: com.mysql.jdbc.Driver
                 username: uoko
                 password: MdmgKSFdUZwK
                 type: com.alibaba.druid.pool.DruidDataSource
                 druid:
                   max-active: 20
                   initial-size: 1
                   max-wait: 60000
                   min-idle: 3
                   remove-abandoned: true
                   remove-abandoned-timeout: 180
                   connection-properties:
                   client-encoding: UTF-8
                   test-while-idle: true
          ```  
        
        *  redis
            
          redis 需连接到 
          ```
           spring:
              redis:
                host: 192.168.200.121
                port: 6379
                database: 3
          ```
          
        * rabbitmq
          
          rabbitmq 需连接到 
          ```
           spring:
             rabbitmq:
               host: 192.168.200.122
               port: 5672
               username: admin
               password: abcd1234
          
          ```

        
* jenkins 发布
  
  jenkins发布，点击 [http://192.168.200.120:8080/jenkins](http://192.168.200.120:8080/jenkins)
  登录账号 `dev_admin`,`dev_admin`,寻找到相应的应用点击发布即可。
  **注意事项：如发现jenkins上没有自己的服务，请联系`先果`协助添加应用**
  
             
      