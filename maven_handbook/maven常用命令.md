# maven常用命令

3. 查看maven树
    ```
    mvn  dependency:tree>tree.txt   
    ```

4. 编译源代码：
    ```
    mvn compile
    ```
    
5. 编译测试代码：
    ```
     mvn test-compile
    ```
    
6. 运行测试:
    ```
    mvn test
    ```
    
7. 产生site：
    ```
    mvn site
    ```
    
8. 打包：
    ```
    mvn package
    ```
9. 在本地Repository中安装jar：
    ```
    mvn install
    ```
例：installing D:\xxx\xx.jar to D:\xx\xxxx

10. 清除产生的项目：
    ```
    mvn clean
    ```

13. 组合使用goal命令，如只打包不测试：
    ```
    mvn -Dtest package
    或者
    mvn -Dmaven.test.skip=true package
    ```
    
14. 编译测试的内容：
    ```
    mvn test-compile
    ```
    
15. 只打jar包:
    ```
    mvn jar:jar
    ```
16. 只测试而不编译，也不测试编译：
    ```
    mvn test -skipping compile -skipping test-compile
    ( -skipping 的灵活运用，当然也可以用于其他组合命令) 
     ```

18.查看当前项目已被解析的依赖：
    ```
    mvn dependency:list
    ```
19.上传到私服：
    ```
    mvn deploy
    ```
20. 强制检查更新，由于快照版本的更新策略(一天更新几次、隔段时间更新一次)存在，如果想强制更新就会用到此命令: 
    ```
    mvn clean install-U
    ```
    
21. 源码打包：
    ```
    mvn source:jar
    或
    mvn source:jar-no-fork
    ```