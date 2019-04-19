# 使用中台api

使用中台api，只需要简单几步即可完成。

   1. 引入jar包
       ```
       <dependency>
          <groupId>com.uoko.uc.api</groupId>
          <artifactId>uc-module-api</artifactId>
          <version>1.0-SNAPSHOT</version>
        </dependency>        
       ``` 
       
   2. 添加配置(yml)
       ```
       uoko:
         endpoint:
           uc: uoko-platform-uc       
       ``` 
       
   3. 配置fegin client 扫描
       ```
       @EnableFeignClients({"com.uoko.uc"})     
       ``` 
   4. 初始化client
       ```
       ribbon:
         #请求处理的超时时间
         ReadTimeout: 120000
         #请求连接的超时时间
         ConnectTimeout: 120000
         eager-load:
           enabled: true
           clients: uoko-platform-uc 
       ``` 