# core层service

core层service，在目前架构中定义成：用来实现`uoko-xxx-xxx-api`中接口的实现。

 * 案例
    
  ```
   @RequestMapping("user")
   @RestController()
   @Api(value = "用户管理", description = "用户中心用户模块")
   @Service
   public class UcUserServiceImpl implements UserService {
   
       @Autowired
       private UcUserDataService ucUserDataService;
       @Autowired
       private UcRoleDataService ucRoleDataService;
       @Autowired
       private UcPlatformDataService ucPlatformDataService;
       @Autowired
       private UcPlatformRoleDataService ucPlatformRoleDataService;
       @Autowired
       private UcAuthDataService ucAuthDataService;
       @Autowired
       private UcExtraDataService ucExtraDataService;
       @Autowired
       private UcAuthPlatformDataService ucAuthPlatformDataService;
       @Autowired
       private BCryptPasswordEncoder bCryptPasswordEncoder;
       @Autowired
       private SnowFlake snowFlake;
       @Autowired
       private UcUserPlatformDataService ucUserPlatformDataService;
       
       @ApiOperation("用户id查询用户信息")
       @ApiImplicitParam(value = "用户id", name = "userId", dataType = "Long", example = "12111")
       @GetMapping("{userId}")
       @Override
       public UserDTO findUserByUserId(@PathVariable("userId") String userId) {
           /*
           1.查询用户基本数据
           2.查询用户额外数据
            */
           UcUserEntity ucUserEntity = ucUserDataService.selectById(userId);
           if (ucUserEntity == null) {
               return null;
           }
           UserDTO userDTO = new UserDTO();
           BeanUtils.copyProperties(ucUserEntity, userDTO);
           userDTO.setUserId(ucUserEntity.getId());
           UcExtraEntity ucExtraEntity = ucExtraDataService.findByUserId(ucUserEntity.getId());
           UcExtraDTO ucExtraDTO = new UcExtraDTO();
           BeanUtils.copyProperties(ucExtraEntity, ucExtraDTO);
           userDTO.setUcExtraDTO(ucExtraDTO);
           return userDTO;
       }
   
       /**
        * 用户存在，不存在授权的账号
        * 1.判断是否有授权账号
        * 2.如果无注册
        * 3.如果有返回已经存在
        * 4.是否是新平台同一个账号加入
        * <p>
        * 用户不存在
        * 1.插入用户表
        * 2.插入额外的信息
        * 3.插入授权信息
        * 4.分配平台
        *
        * @param
        * @return
        * @author shaohua
        * @date
        **/
       @Override
       @ApiOperation(value = "增加用户信息")
       @PostMapping
       @Transactional(rollbackFor = Exception.class)
       public UserDTO insertUser(@RequestBody @Valid UserDTO userDTO) {
           UcUserEntity ucUserEntity = ucUserDataService.findUserByUsername(userDTO.getUsername());
           if (ucUserEntity != null) {
               //用户存在，检查用户是否有更新数据，或者确实数据
               return updateUserInfo(userDTO, ucUserEntity);
           } else {
               //用户不存在 插入用户数据
               return insertUserInfo(userDTO);
           }
       }
    } 

  ```