# config

config目录，在目前项目架构中定义内容稍微比较广泛。它们分别包含。

   1. 读取配置文件(.yml)
   2. bean注入(纳入spring容器进行管理)
   3. 其他组件的配置信息
   4. 等等


1. 读取配置文件(.yml)
  
  * 读取配置信息
    
    * 案例1
    
        * 配置yml内容
          ```
          ignore:
            urls:
              - /actuator/health
              - /actuator/env
              - /actuator/scheduledtasks
              - /oauth/token
              - /oauth/authorize
              - /login
              - /mobile/**
              - /http/**
              - /swagger-resources/**
              - /swagger-ui.html
              - /*/v2/api-docs
              - /swagger/api-docs
              - /oauth/token_key
              - /webjars/**
              - /actuator/threaddump
              - /auth/**
            clients:
              - app
        
          ```    
        
        * 读取配置class
        
          ```
          @Data
          @Configuration
          @RefreshScope
          @ConditionalOnExpression("!'${ignore}'.isEmpty()")
          @ConfigurationProperties(prefix = "ignore")
          public class FilterIgnorePropertiesConfig {
          
              private List<String> urls = new ArrayList<>();
          
              private List<String> clients = new ArrayList<>();
          }
        
          ```   

    * 案例2
      
      ```
       @Value("${spring.application.name:unknown}")
           private String applicationName;
      ```
    


2. bean注入(纳入spring容器进行管理)

  * 新建一个bean类
      ```
      public class SomeBean {
      
      }
    
      ``` 
  
  * bean注入
      ```
      @Configuration
      public class Config {
      
          @Bean
          public SomeBean someBean() {
              return new SomeBean;
          }
      }
    
      ```
  
  * 使用bean
      ```
       @Autowired
       private SomeBean someBean;
      ```


3. 其他组件的配置信息
   
  * 示例
      ```
      @PropertySource("com/spring/db.properties")
      @ComponentScan(basePackages = "com.spring")
      @Configuration
      public class Config {
      
          @Autowired
          private Environment env;
      
          @Bean
          public DataSource dataSource() {
              return new DataSource(env.getProperty("url"),env.getProperty("driverClass"),
                      env.getProperty("user"),env.getProperty("password"));
          }
      }
    
      ```
  
  
  * 示例
  
      ```
      @Order(SecurityProperties.BASIC_AUTH_ORDER - 3)
      @Configuration
      @EnableWebSecurity
      public class SecurityConfigurerAdapter extends WebSecurityConfigurerAdapter {
          @Autowired
          private FilterIgnorePropertiesConfig filterIgnorePropertiesConfig;
          @Autowired
          private MobileSecurityConfigurer mobileSecurityConfigurer;
          @Autowired
          private HttpTokenSecurityConfigurer httpTokenSecurityConfigurer;
          @Autowired
          private UsernameSecurityConfigurer usernameSecurityConfigurer;
          @Autowired
          private OpenIdSecurityConfigurer openIdSecurityConfigurer;
      
          @Override
          protected void configure(HttpSecurity http) throws Exception {
              ExpressionUrlAuthorizationConfigurer<HttpSecurity>.ExpressionInterceptUrlRegistry registry =
                      http.formLogin().loginPage("/authentication/login")
                              .loginProcessingUrl("/authentication/form")
                              .and()
                              .authorizeRequests();
              filterIgnorePropertiesConfig.getUrls().forEach(
                      url -> registry.antMatchers(url).permitAll()
              );
              registry.anyRequest().permitAll()
                      .and()
                      .csrf().disable();
              //http token
              http.apply(httpTokenSecurityConfigurer);
              //手机号码
              http.apply(mobileSecurityConfigurer);
              //星空 op用户
              http.apply(usernameSecurityConfigurer);
              //openid
              http.apply(openIdSecurityConfigurer);
      
      
          }
          @Bean
          @Override
          public AuthenticationManager authenticationManagerBean() throws Exception {
              return super.authenticationManagerBean();
          }
      }
    
      ```