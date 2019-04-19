# 发布uoko-xxx-api

经常在开发中，听见伙伴们说：`为啥我的api别人无法调用，而你的可以啦？`。

其实这个问题就是个简单的问题，**因为你的api为发布**

 * api发布 
    
    * 开发阶段
        
        api在开发阶段，请不要发布`RELEASE`版本，发布`SNAPSHOT`版本。
        SNAPSHOT：可以无限次覆盖；RELEASE：只能发布一次，下一次发布必须升级版本。
   
    * 执行maven命令
        
        ```
         mvn clean deploy
        ```