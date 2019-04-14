# Spring Boot 配置文件

---

## Spring Boot 支持两种格式的配置文件

1. .properties 格式的配置文件\(键值对的形式\)

```
# 配置服务器端口号
server.port=9080
# 配置应用的访问路径(虚拟目录)
server.servlet.context-path=/springboot-web
```

1. .yml 或者 .yaml格式的配置文件\(yml语言格式\)

```
server:
# 配置服务器端口号
  port: 9080
  servlet:
# 配置应用的访问路径(虚拟目录)
    context-path: /springboot-web
```

> 如果同时存在 appliction.properties 和 appliction.yml 配置文件的话,优先使用 appliction.properties 中的配置



