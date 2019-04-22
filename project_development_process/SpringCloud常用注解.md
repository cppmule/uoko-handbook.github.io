# SpringCloud常用注解

* 验证类型 的注解
   
 * @EnableDiscoveryClient
 
    让服务发现服务器,使用服务器.Spring cloud 实现服务发现
    
 * @EnableFeignClients(
        basePackages = {
        "com.uoko.push", 
        "com.uoko.uc", 
        "com.uoko.base.data",
        "com.uoko.house"
        })
     
    开启feign客户端，需要扫描的包 basePackages
     
 * @FeignClient(name = "${uoko.endpoint.partner}")
   
   feign客户端注解。作用于api
 
 * @EnableZuulProxy
   
   Zuul网管注解 
 
 * @LoadBalanced	
 
   开启负载均衡（客户端） 配合@EnableFeignClients
   
 * @EnableHystrix
   
   表示启动断路器，断路器依赖于服务注册和发现。
 
 * @HystrixCommand
   
   注解方法失败后，系统将西东切换到fallbackMethod方法执行