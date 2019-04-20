# dao

dao层，在目前架构中，仅用来存放mybatis中的dao。

   * 示例
   
   ```
   @Mapper
   public interface UcUserDao extends BaseMapper<UcUserEntity> {
       /**
        * 通过账号查询用户信息
        *
        * @param username 用户名
        * @return
        */
       UcUserEntity selectByUsername(@Param("username") String username);
   
       /**
        * 通过用户手机号查询用户信息
        *
        * @param phone    用户账号
        * @param platform 平台
        * @return
        */
       UcUserEntity findUserByPhoneAndPlatform(@Param("phone") String phone,
                                               @Param("platform_name") String platform);
   
       /**
        * userId批量查询
        *
        * @param userIds userIds
        * @return
        * @author shaohua
        * @date
        **/
       List<UcUserEntity> findByUserIds(String... userIds);
   
       /**
        * 多条件查询用户信息
        *
        * @param username     用户名(用户手机号|用户名)
        * @param realName     用户真实姓名
        * @throws
        * @author shaohua
        * @date 2019/2/27 19:31
        */
       List<UcUserPlatformPO> findByUsers(@Param("username") String username,
                                          @Param("realName") String realName);
   }

    ```
   