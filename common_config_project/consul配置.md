# consul配置

consul 在目前微服务架构中扮演者比较重要的角色，承接着服务与服务之间的发现，也就是常说的
`服务注册发现`。接下来将介绍目前微服务中三套环境的不同consul配置。

* 开发环境(dev)
    
    取消本地应用注册到consul上。
    添加以下配置，当前环境下的服务将不会注册到consul上，
    这样其他机器的服务调用也不会调用到本机服务。开发中可以按需添加此类配置。
    ```
     cloud:
        service-registry:
          auto-registration:
            enabled: false
    ```
 
    完整配置如下。
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

* 测试环境(test)

   在目前的环境配置中，测试环境的配置文件不在项目内部管理，而是通过config服务远程管理，
   如果需要修改配置，需要修改config中git仓库的配置。
   
   git仓库中配置如下。
    ```
      cloud:
        consul:
          host: 192.168.200.27
          port: 8500
          discovery:
            healthCheckPath: /actuator/health
            healthCheckInterval: 5s
            enabled: true
            prefer-ip-address: true
          enabled: true
    ```
 
* 预发布环境(pre)
    
   在目前的环境配置中，测试环境的配置文件不在项目内部管理，而是通过config服务远程管理，
   如果需要修改配置，需要修改config中git仓库的配置。
 
   git仓库中配置如下。
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
 
* 发布环境(prod)
    
   在目前的环境配置中，测试环境的配置文件不在项目内部管理，而是通过config服务远程管理，
   如果需要修改配置，需要修改config中git仓库的配置。
 
   git仓库中配置如下。
    ```
      cloud:
        consul:
          host: 10.0.0.175
          port: 8500
          discovery:
            healthCheckPath: /actuator/health
            healthCheckInterval: 5s
            enabled: true
            prefer-ip-address: true
          enabled: true
    ```
