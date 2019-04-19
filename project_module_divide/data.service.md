# data.service

data.service层，在目前架构中，主要用来连通dao和core层service的传递层。

 * 示例
    ```
    @Service
    public class UcAuthDataServiceImpl extends ServiceImpl<UcAuthDao, UcAuthEntity> implements UcAuthDataService {
    
        @Autowired
        private UcAuthDao ucAuthDao;
    
        @Override
        public PageUtils queryPage(Map<String, Object> params) {
            Page<UcAuthEntity> page = this.selectPage(
                    new Query<UcAuthEntity>(params).getPage(),
                    new EntityWrapper<UcAuthEntity>()
            );
    
            return new PageUtils(page);
        }
    
        @Override
        public UcAuthEntity findByIdentifier(String identifier) {
            return ucAuthDao.findByIdentifier(identifier);
        }
    
        @Override
        public List<UcAuthEntity> findByUserId(String userId) {
            return ucAuthDao.findByUserId(userId);
        }
    
    }
    ```
