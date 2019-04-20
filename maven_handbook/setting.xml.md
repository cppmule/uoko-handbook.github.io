# setting.xml

setting.xml，是个比较重要的文件，它管理者我们本地仓库地址、账号、远程仓库地址等信息。

* setting.xml 文件

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
        
        <localRepository>C:/software/java/maven/repository</localRepository>
    
        <servers>
            <server>
                <id>nexus-releases</id>
                <username>uoko</username>
                <password>P@ssw0rd</password>
            </server>
        </servers>
    
        <mirrors>
            <mirror>
                <id>mirrorId</id>
                <mirrorOf>repositoryId</mirrorOf>
                <name>Human Readable Name for this Mirror.</name>
                <url>http://my.repository.com/repo/path</url>
            </mirror>
    
            <mirror>
                <id>nexus-uoko</id>
                <mirrorOf>aliyun</mirrorOf>
                <name>uoko aliyun repository</name>
                <url>http://172.16.0.141:8081/nexus/content/groups/public/</url>
            </mirror>
        </mirrors>
        
        <profiles>
            <profile>
                <id>jdk-1.8</id>
                <activation>
                    <activeByDefault>true</activeByDefault>
                    <jdk>1.8</jdk>
                </activation>
                <properties>
                    <maven.compiler.source>1.8</maven.compiler.source>
                    <maven.compiler.target>1.8</maven.compiler.target>
                    <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
                </properties>
            </profile>
        </profiles>
         
    </settings>
    
    ```   
