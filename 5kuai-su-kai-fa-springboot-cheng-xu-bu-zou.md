# 快速开发springboot程序步骤

* 创建一个spring boot 项目

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



