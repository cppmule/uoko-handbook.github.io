# bootstap.xml配置

bootstrap.xml 在目前微服务启动时，用来获取远程配置，并覆盖本地配置的文件。

* 开发环境(dev)
    
    开发环境由于开发过程经常修改配置，因此目前不走config配置。本地开发需要检查`config`是否关闭，
    需要将 config 关闭 `enabled: false`。
    
    如下配置。
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
 

* 测试环境(test)

   在目前的环境配置中，需要走config配置中心，因此需要开启config中心获取配置阈`enabled: true`,
   将uri修改成对应的环境config配置中心地址。最后比较总要的是检查name是否是当前应用的`application.name`,
   `uoko-system-common`是必填的，此处添加即可无需关心它有何用。
   
   配置如下。
   
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
 
* 预发布环境(pre)
    
   在目前的环境配置中，需要走config配置中心，因此需要开启config中心获取配置阈`enabled: true`,
   将uri修改成对应的环境config配置中心地址。最后比较总要的是检查name是否是当前应用的`application.name`,
 
   
    ```
      spring:
        cloud:
          config:
            uri: http://10.0.0.218:8040
            name: uoko-platform-auth,uoko-system-common
            profile: pro
            label: master
            enabled: true
    ```
 
* 发布环境(prod)
    
   在目前的环境配置中，需要走config配置中心，因此需要开启config中心获取配置阈`enabled: true`,
   将uri修改成对应的环境config配置中心地址。最后比较总要的是检查name是否是当前应用的`application.name`,
   
    ```
      spring:
        cloud:
          config:
            uri: http://10.0.0.137:8040
            name: uoko-platform-auth,uoko-system-common
            profile: pro
            label: master
            enabled: true
    ```



