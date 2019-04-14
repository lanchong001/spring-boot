# 快速开发springboot程序步骤

* 创建一个spring boot 项目

---

1. 使用eclipse 的 Spring Tool Suite\(STS\) 插件、或者 IDEA自带的插件创建
2. 直接使用Maven创建项目的方式创建

3. POM文件中增加 spring boot parent 依赖,以及其他的启动依赖

```
    <!--继承spring boot的父级项目依赖-->
    <parent>
        <groupId>com.lym.springboot</groupId>
        <artifactId>springboot-demo</artifactId>
        <version>1.0.0</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
```

```
    <!--spring boot web 开发启动依赖-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
```

* 创建Spring boot 的入口main方法，添加@SpringBootApplication注解

```
@SpringBootApplication
public class SpringBootApplication {

    public static void main(String[] args) {
        //启动springboot程序,启动spring容器.如果引用了spring-boot-starter-web的话,默认启动内嵌的tomcat服务器
        SpringApplication.run(SpringBootApplication.class, args);
    }

}
```

* 创建一个Spring MVC 的 Controler类

```
@RestController
@RequestMapping("/helloworld")
public class HelloWorldController {
    @GetMapping("/hi}")
    public String (){
       return "Hi, Spring Boot!";
    }
}
```

# 

# Spring Boot 脚手架相关的特征

---

1. spring boot 项目必须配置父级依赖 spring-boot-starter-parent , 配置了spring-boot-starter-parent父级依赖,则表明当前项目为Spring Boot 项目
2. spring-boot-starter-parent 是一个特殊的starter依赖,它包含常用功能的 maven jar 包依赖,并且已经制定了jar包的版本.因此,spring boot 项目使用相关功能时,只需要提供 groupId 和 artifactId,而不需要提供 version

3. spring boot 中提供了那些默认的jar包依赖及版本,可以在该父级依赖的pom文件中找到

4. ```
   //spring-boot-dependencies-2.1.4.RELEASE.pom 中列出的常用依赖版本号
   <properties>
       <activemq.version>5.15.9</activemq.version>
       <activemq.version>5.15.9</activemq.version>
       <antlr2.version>2.7.7</antlr2.version>
       <appengine-sdk.version>1.9.73</appengine-sdk.version>
       <artemis.version>2.6.4</artemis.version>
       <aspectj.version>1.9.2</aspectj.version>
       <assertj.version>3.11.1</assertj.version>
       <atomikos.version>4.0.6</atomikos.version>
       <bitronix.version>2.1.4</bitronix.version>
       <build-helper-maven-plugin.version>3.0.0</build-helper-maven-plugin.version>
       <byte-buddy.version>1.9.12</byte-buddy.version>
       <caffeine.version>2.6.2</caffeine.version>
       <cassandra-driver.version>3.6.0</cassandra-driver.version>
       <classmate.version>1.4.0</classmate.version>
       <commons-codec.version>1.11</commons-codec.version>
       <commons-dbcp2.version>2.5.0</commons-dbcp2.version>
       <commons-lang3.version>3.8.1</commons-lang3.version>
       <commons-pool.version>1.6</commons-pool.version>
       <commons-pool2.version>2.6.1</commons-pool2.version>   
       ...
   <properties>
   ```
5. 如果不想使用某个默认的依赖,可以通过pom文件的属性配置覆盖各个依赖项

```
//采用 5.15.8 覆盖 spring boot 默认的 activemq版本
<properties>
    <activemq.version>5.15.8</activemq.version>
<properties>
```

1. @SpringBootAppliction 注解 是SpringBoot项目的核心注解,主要作用是启动Spring的自动配置

```
package com.lym.springboot.maven.springboot.web;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MavenSpringBootWebAppliction {
    public static void main(String[] args) {
        //启动springboot程序,启动spring容器.如果引用了spring-boot-starter-web的话,默认启动内嵌的tomcat服务器
        SpringApplication.run(MavenSpringBootWebAppliction.class);
    }
}
//其他的带有配置项或者注解@Controller,@RestController,@Service,@Compoment,@Repository,@Mapper的类必须是com.lym.springboot.maven.springboot.web
包和子包里面, Spring Boot 的自动配置,包扫描,Bean注入才会有效果.否则,提示找不到对应的对象
```

1. main方法是一个标准的java程序的main方法,主要作用是作为项目启动运行得入口
2. Spring Boot Web 项目依然是使用 Spring + Spring MVC 相关的库



