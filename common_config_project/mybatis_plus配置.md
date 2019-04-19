# mybatis-plus配置.md

mybatis-plus是一个 MyBatis 的增强ORM工具。在选型中由于各种特点被直接纳入项目中使用。
在使用中，只需要在配置文件中简单的添加配置，在`resources`中创建`mapper`来存放我们的xml文件，
在`com.uoko.xxx`包下创建`dao`用来存储查询的接口，最后需要添加`dao`扫描器
`@MapperScan(basePackages = "com.uoko.xxx.xxx.dao")`,到此即配置完mybatis-plus。

* mybatis-plus 配置文件配置
    
    **注意事项：开发过程需要检查 `mapper-locations`扫描mapper.xml是否路径正确，`typeAliasesPackage` 是否扫描entity路径**
   
   ```
    # Mybatis配置
    mybatis-plus:
      mapper-locations: classpath:/mapper/**Mapper.xml
      #实体扫描，多个package用逗号或者分号分隔
      typeAliasesPackage: com.uoko.xxx.xxx.domain.entity
      global-config:
        #主键类型  0:"数据库ID自增", 1:"用户输入ID",2:"全局唯一ID (数字类型唯一ID)", 3:"全局唯一ID UUID";
        id-type: 1
        #字段策略 0:"忽略判断",1:"非 NULL 判断"),2:"非空判断"
        field-strategy: 2
        #驼峰下划线转换
        db-column-underline: true
        #刷新mapper 调试神器
        refresh-mapper: true
        #逻辑删除配置（下面3个配置）
        logic-delete-value: 1
        logic-not-delete-value: 0
      configuration:
        map-underscore-to-camel-case: true
        cache-enabled: false
    ```

* mybatis-plus 扫描器配置

   ```
      @MapperScan(basePackages = "com.uoko.xxx.xxx.dao")
   ```
   配置如图：
   
    ![mybatis-plus扫描器](/img/mybatis_plus_dao.png)