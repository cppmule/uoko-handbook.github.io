# ORM注解
  
* mybatis 注解

  * @Param	
  
    Parameter	N/A	如果你的映射器的方法需要多个参数, 这个注解可以被应用于映射器的方法
  参数来给每个参数一个名字。否则,多 参数将会以它们的顺序位置来被命名 
  (不包括任何 RowBounds 参数) 比如。 #{param1} , #{param2} 等 , 
  这 是 默 认 的 。 使 用 @Param(“person”),参数应该被命名为 #{person}。
    ```
     List<EntrustInfoEntity> findByUserIdAndCityId(@Param("userId") String userId,
                                                     @Param("cityId") String cityId);
    ```
  
  * @MapperScan
    
    指定dao存放路径，用于mybatis扫描使用。
    `@MapperScan(basePackages = {"com.uoko.partner.biz.dao"})`
  
  * @Mapper 
   
    dao标识，加载到bean中管理。
  
  * @TableName
  
    表名注解，指定与数据库表的关联,这里的注解意味着你的数据库里应该有一个名为user的表与之对应
   `@TableName("account_info")`
   
  * @TableId
    
    主键注解。
  
  * @TableField
    
    非主键的字段注解
     * value ：表字段名称，目前我们常用于is_deleted
     * exist: 表中没有的属性需要加注解@TableField(exist = false),表示排除当前类中的属性.
  
  * @Version
  
    乐观锁注解、标记 @Verison 在字段上
  
  * @TableLogic
    
    表字段逻辑处理注解（逻辑删除）
    
     