# spring注解
  
* spring 注解

    * @SpringBootApplication
    
      包含了@ComponentScan、@Configuration和@EnableAutoConfiguration注解。
      其中@ComponentScan让spring Boot扫描到Configuration类并把它加入到程序上下文。

    * @Configuration 
    
      等同于spring的XML配置文件；使用Java代码可以检查类型安全。将配置信息bean管理化。
      
      相当于传统的xml配置文件，如果有些第三方库需要用到xml文件，建议仍然通过@Configuration类作为项目的配置主类——可以使用@ImportResource注解加载xml配置文件。

    * @EnableAutoConfiguration 
    
      自动配置，默然我们添加 `@SpringBootApplication`自动开启。
      
      Spring Boot自动配置（auto-configuration）：尝试根据你添加的jar依赖自动配置你的Spring应用。例如，如果你的classpath下存在HSQLDB，并且你没有手动配置任何数据库连接beans，那么我们将自动配置一个内存型（in-memory）数据库”。你可以将@EnableAutoConfiguration或者@SpringBootApplication注解添加到一个@Configuration类上来选择自动配置。如果发现应用了你不想要的特定自动配置类，你可以使用@EnableAutoConfiguration注解的排除属性来禁用它们。

    * @ComponentScan 
      
      组件扫描，可自动发现和装配一些Bean。可以配置扫描包范围，例如 `@ComponentScan("com.uoko")`
      
      表示将该类自动发现扫描组件。个人理解相当于，如果扫描到有@Component、@Controller、@Service等这些注解的类，并注册为Bean，可以自动收集所有的Spring组件，包括@Configuration类。我们经常使用@ComponentScan注解搜索beans，并结合@Autowired注解导入。可以自动收集所有的Spring组件，包括@Configuration类。我们经常使用@ComponentScan注解搜索beans，并结合@Autowired注解导入。如果没有配置的话，Spring Boot会扫描启动类所在包下以及子包下的使用了@Service,@Repository等注解的类。

    * @Component
      
      泛指组件，某个bean不是service、configuration 既不是mapper便可使用此注解。

    * @RestController
    
      @RestController注解是@Controller和@ResponseBody的合集,
      表示这是个控制器bean,并且是将函数的返回值直 
      接填入HTTP响应体中,是REST风格的控制器。

    * @Autowired
   
      自动导入依赖的bean。byType方式。把配置好的Bean拿来用，完成属性、方法的组装，它可以对类成员变量、方法及构造函数进行标注，完成自动装配的工作。当加上（required=false）时，就算找不到bean也不报错。

    * @Import
    
      用来导入其他配置类。
   
    * @ImportResource
      
      用来加载xml配置文件。
   
   * @Service
   
      一般用于修饰service层的组件
   
   * @Repository
   
     使用@Repository注解可以确保DAO或者repositories提供异常转译，这个注解修饰的DAO或者repositories类会被ComponetScan发现并配置，同时也不需要为它们提供XML配置项。
   
   * @Bean
     
     用@Bean标注方法等价于XML中配置的bean。
   
   * @Value
     
     注入Spring boot application.properties配置的属性的值。示例代码：
     ```
       @Value(value = “#{spring.application.name:unknown}”) 
       private String applicationName;
     ```
   
   * @Bean
   
     相当于XML中的,放在方法的上面，而不是类，意思是产生一个bean,并交给spring管理。
   
   * @Qualifier
     
     当有多个同一类型的Bean时，可以用@Qualifier(“name”)来指定。与@Autowired配合使用。
     @Qualifier限定描述符除了能根据名字进行注入，但能进行更细粒度的控制如何选择候选者，具体使用方式如下：
     ```
       @Autowired 
       @Qualifier(value = "opInfoService") 
       private OpInfoService opInfoService;
     ```
   * @Resource(name="name",type="type")
   
     没有括号内内容的话，默认byName。与@Autowired干类似的事。
   
   * @Inject
    
     等价于默认的@Autowired，只是没有required属性,目前我们未开起
     
   * @ControllerAdvice
        
    包含@Component。可以被扫描到。统一处理异常。

   * @ExceptionHandler(Exception.class)
    
    用在方法上面表示遇到这个异常就执行以下方法

   * @Scope
   
     作用域。
   
   * @Async 
   
     异步方法调用,springboot中需要开启Async配置`@EnableAsync`
     
   * @PostConstruct
     
      初始化注解，可以在程序运行时执行。
      ```
        /**
         * Callback used to run the bean.
         * 初始化路由配置的数据
         */
        @PostConstruct
        public void init() {
            log.info("开始初始化路由配置数据");
            List<SysZuulRouteEntity> routeList = sysZuulRouteService.selectList(new EntityWrapper<>());
            if (CollUtil.isNotEmpty(routeList)) {
                redisTemplate.opsForValue().set(CommonConstant.ROUTE_KEY, routeList);
                log.info("更新Redis中路由配置数据：{}条", routeList.size());
            }
            log.info("初始化路由配置数据完毕");
    
            log.info("开始初始化【权限路径】配置数据");
            Set<MenuDTO> menuDTOS = menuService.findByIgnoreUrl();
            if (CollUtil.isNotEmpty(menuDTOS)) {
                redisTemplate.opsForValue().set(CommonConstant.IGNORE_URL_KEY, menuDTOS);
                log.info("更新Redis中【权限路径】配置数据：{}条", menuDTOS.size());
            }
            log.info("开始初始化权【权限路径】配置数据完毕");
        }  
      ```
   
   * @PreDestroy
   
     摧毁注解 默认 单例
    
   * @Transcational
    
     事务处理
   
   * @EnableTransactionManagement 
   
    spring boot 开启对注解式事物的支持
   
   * @EnableAaspectJAutoProxy 
     
     开启Spring 对 这个切面(Aspect )的支持
     
   * @Aspect 
   
     声明这是一个切面 
   
   * @After 
   
   * @Before
   
   
   * @Around 
   
     定义切面,可以直接将拦截规则(切入点 PointCut)作为参数
   
   * @PointCut 
    
     专门定义拦截规则 然后在 @After @Before. @Around 中调用
   