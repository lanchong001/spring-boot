# 快速开发springboot程序步骤

* 创建一个spring boot 项目

---

1. 使用eclipse 的 Spring Tool Suite\(STS\) 插件、或者 IDEA自带的插件创建
2. 直接使用Maven创建项目的方式创建

* POM文件中增加 spring boot parent 依赖,以及其他的启动依赖

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



