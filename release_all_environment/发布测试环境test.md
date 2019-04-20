# 发布测试环境(test)

测试环境(test)
1. 测试环境管理相对规范，资源分配均匀。测试目前服务器由`子衡`统一管控。
如有新服务需要部署，需要联系`子衡`协助.
2. 测试环境采用config配置中心，因此配置将会走测试环境配置中心。

目前部署应用服务的服务器清单。

IP|	OS|	root密码|	port|	操作账号|	操作密码|作用
---|---|---|---|---|---|---
192.168.200.126|	centos7.5|	-|	22|	    arch-uoko|	archUoko@123|X端开发占用中
192.168.200.44|  	centos7.5|        -|	 22|	arch-uoko|	archUoko@123|基础组件占用中
192.168.200.45|  	centos7.5|        -|	 22|	arch-uoko|	archUoko@123|可部署其他服务
192.168.200.46|  	centos7.5|        -|	 22|	arch-uoko|	archUoko@123|可部署其他开发服务

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
                 uri: http://192.168.200.26:8040
                 name: uoko-platform-auth,uoko-system-common
                 profile: pro
                 label: master
                 enabled: true

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
          
          mysql 需连接到 ```192.169.200.66:3336```  
        
        *  redis
            
          redis 需连接到 ```192.168.200.121:```
          
        * rabbitmq

* jenkins 发布
  
  jenkins发布，点击 [http://192.168.200.120:8080/jenkins](http://192.168.200.120:8080/jenkins)
  登录账号 `test_admin`,`test_admin`,寻找到相应的应用点击发布即可。
    **注意事项：如发现jenkins上没有自己的服务，请联系`先果`或`子衡`协助添加应用**