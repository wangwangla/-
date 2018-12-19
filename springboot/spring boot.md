---
title: spring boot
user: 见贤思齐
date: 2018-12-19
---
Spring Boot依赖使用的groupId为org.springframework.boot。通常，你的Maven POM文件会继承spring-boot-starter-parent工程，Spring Boot提供了一个可选的Maven插件，用于创建可执行jars。
**依赖继承**
```
<parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>1.4.0.BUILD-SNAPSHOT</version>
</parent>
```

web依赖
```
 <!-- Add typical dependencies for a web application -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
   </dependencies>
```
插件
```
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```
**gradle**
```
buildscript {
    repositories {
        jcenter()
		写仓库
        maven { url "http://repo.spring.io/snapshot" }
        maven { url "http://repo.spring.io/milestone" }
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.4.0.BUILD-SNAPSHOT")
    }
}

apply plugin: 'java'
apply plugin: 'spring-boot'

jar {
    baseName = 'myproject'
    version =  '0.0.1-SNAPSHOT'
}

repositories {
    jcenter()
    maven { url "http://repo.spring.io/snapshot" }
    maven { url "http://repo.spring.io/milestone" }
}

dependencies {
    compile("org.springframework.boot:spring-boot-starter-web")
    testCompile("org.springframework.boot:spring-boot-starter-test")
}
```
**CLI**
Spring Boot CLI是一个命令行工具，可用于快速搭建基于Spring的原型。它支持运行Groovy脚本，这也就意味着你可以使用类似Java的语法，但不用写很多的模板代码。
安装
Spring CLI分发包可以从Spring软件仓库下载：
spring-boot-cli-1.4.0.BUILD-SNAPSHOT-bin.zip
spring-boot-cli-1.4.0.BUILD-SNAPSHOT-bin.tar.gz
不稳定的snapshot分发包也可以获取到。
下载完成后，解压分发包，根据存档里的INSTALL.txt操作指南进行安装。总的来说，在.zip文件的bin/目录下会有一个spring脚本（Windows下是spring.bat），或使用java -jar运行lib/目录下的.jar文件（该脚本会帮你确保classpath被正确设置）。

**运行**
```
到此，示例应用可以工作了。由于使用了spring-boot-starter-parent POM，这样我们就有了一个非常有用的run目标来启动程序。在项目根目录下输入mvn spring-boot:run启动应用：
```

jar的方式运行
```
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```
保存pom.xml，并从命令行运行mvn package
- 运行
 java -jar target/myproject-0.0.1-SNAPSHOT.jar
1