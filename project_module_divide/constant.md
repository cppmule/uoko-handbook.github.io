# constant

constant根据它的意思“不变的”，这个目录用来存放全部静态常量。

 * 案例
    ```
    public interface SecurityConstants {
        /**
         * 手机号授权地址
         */
        String MOBILE_TOKEN_URL = "/mobile/token";
    
        /**
         * 手机号授权地址
         */
        String OPENID_TOKEN_URL = "/openid/token";
        /**
         * 密码+账号授权地址
         */
        String USERNAME_TOKEN_URL = "/username/token";
    
        /**
         * 携带三方token授权地址
         */
        String HTTP_TOKEN_URL = "/http/token";
    
        /**
         * username 授权地址
         */
        String OAUTH2_TOKEN_URL = "/oauth/token";
    
        /**
         * 删除
         */
        String STATUS_DEL = "1";
        /**
         * 正常
         */
        String STATUS_NORMAL = "0";
    
        /**
         * 锁定
         */
        String STATUS_LOCK = "9";
    
        /**
         * token-uservo
         */
        String TOKEN_USER_DETAIL = "token-user-detail";
        /**
         * token请求头名称
         */
        String REQ_HEADER = "Authorization";
    
        /**
         * token分割符
         */
        String TOKEN_SPLIT = "Bearer ";
    
        /**
         * jwt签名
         */
        String SIGN_KEY = "UOKO";
    
        /**
         * 路由信息Redis保存的key
         */
        String ROUTE_KEY = "_ROUTE_KEY";
    }
    ```

