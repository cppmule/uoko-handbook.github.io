# maven常用命令

1. 查看maven树
    ```
    mvn  dependency:tree>tree.txt   
    ```
2. 编译源代码：
    ```
    mvn compile
    ```
3. 编译测试代码：
    ```
     mvn test-compile
    ```
4. 运行测试:
    ```
    mvn test
    ```
5. 产生site：
    ```
    mvn site
    ``` 
6. 打包：
    ```
    mvn package
    ```
7. 在本地Repository中安装jar：
    ```
    mvn install
    ```
例：installing D:\xxx\xx.jar to D:\xx\xxxx

8. 清除产生的项目：
    ```
    mvn clean
    ```
9. 组合使用goal命令，如只打包不测试：
    ```
    mvn -Dtest package
    或者
    mvn -Dmaven.test.skip=true package
    ```
10. 编译测试的内容：
    ```
    mvn test-compile
    ```
11. 只打jar包:
    ```
    mvn jar:jar
    ``` 
12. 只测试而不编译，也不测试编译：
    ```
    mvn test -skipping compile -skipping test-compile
    ( -skipping 的灵活运用，当然也可以用于其他组合命令) 
    ```
13.查看当前项目已被解析的依赖：
    ```
    mvn dependency:list
    ```
14.上传到私服：
    ```
    mvn deploy
    
    ```
15. 强制检查更新，由于快照版本的更新策略(一天更新几次、隔段时间更新一次)存在，如果想强制更新就会用到此命令: 
    ```
    mvn clean install-U
    
    ```
16. 源码打包：
    ```
    mvn source:jar
    或
    mvn source:jar-no-fork
    ```