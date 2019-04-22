# 发布预发布环境(pre)

预发布环境(pre)
1. 预发布环境管理相对规范，资源分配均匀。目前服务器由`先果`、`子衡`统一管控。
如有新服务需要部署，需要联系`先果`、`子衡`协助.
2. 预发布环境采用config配置中心，因此配置将会走预发布环境配置中心。
**注意事项：预发布环境部署在公有云上，需要vpn访问，修改配置请找`先果`协助**

* 配置信息检查
   
    * bootstrap.xml配置
      
      bootstrap.xml中的配置，在生成代码过程中是默认开启。需要开发人员检查。
      需将config开启， `spring.cloud.config.enabled: true`。
      (**片外: base 1.1.4.RELEASE 以后版本，bootstrap文件存放在prod文件**)
      
      修改后的配置如下。
      
      ```
       spring:
             cloud:
               config:
                 uri: http://10.0.0.228:8040
                 name: uoko-platform-auth,uoko-system-common
                 profile: pro
                 label: master
                 enabled: true

      ```
    
    * consul配置检查
    
        ```
          cloud:
            consul:
              host: 10.0.0.81
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
               url: jdbc:mysql://10.0.0.164:3336/uk_arch_push?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&useAffectedRows=true&zeroDateTimeBehavior=convertToNull&allowMultiQueries=true&useSSL=true
               username: push
               password: quei]w6pu7ooD4ubahth
               type: com.alibaba.druid.pool.DruidDataSource
               druid:
                 max-active: 20
                 initial-size: 1
                 max-wait: 60000
                 min-idle: 3
                 remove-abandoned: true
                 remove-abandoned-timeout: 180
                 connection-properties:
                 clientEncoding: UTF-8
                 test-while-idle: false
                 enabled: true 
          ```
        
        *  redis
            
         redis 需连接到 
         ```
           spring:
            redis:
              host: 10.0.0.185
              port: 6379
              database: 1
         ```
          
        * rabbitmq
        
        rabbitmq 需连接到 
         ```
          spring:
           rabbitmq:
             host: 10.0.0.81
             port: 5672
             username: uoko_pre
             password: uoko123

         ```

* jenkins 发布
    预发布环境不对开发级别开放，目前由`子衡`和`先果`共同发布，需要发布请联系

