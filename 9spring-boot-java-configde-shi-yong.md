# Spring Boot Java Config 的使用

---

1. @Configuration : 标识当前类为一个配置类
2. @CompomentScan : 用来扫描指定命名空间下的注解类
3. @Import : 用来导入其他的带有@Configuration注解的类\(导入其他配置类\)
4. @ImportResource : 导入xml配置文件
5. @Bean : 用来定义一个bean , 可以指定init\(\),destory\(\)方法,指定bean的范围

[https://blog.csdn.net/moakun/article/details/80178330](https://blog.csdn.net/moakun/article/details/80178330)

---

* 当 java config 所在的类与单元测试类不再同一个命名空间内时，需要在运行单元测试的上下文中配置 java config 类

```
package com.lym.springboot.javaconfig;

import com.lym.springboot.javaconfig.config.Config;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringRunner;
import javax.annotation.Resource;


@RunWith(SpringRunner.class)
@SpringBootTest(classes = Config.class)
@ContextConfiguration(classes = Config.class)
public class ConfigTest {

    //Unable to find a @SpringBootConfiguration, you need to use @ContextConfiguration or @SpringBootTest(classes=...) with your test
    //单元测试时, @SpringBootTest(classes = Config.class) 和 @ContextConfiguration(classes = Config.class) 两者有一个配置就可以执行单元测试

    //DoWorkBean在com.lym.springboot.javaconfig.config.Config目录, 单元测试类在com.lym.springboot.javaconfig.因此,需要指定Java config 配置类
    @Resource
    private DoWorkBean doWorkBean;

    @Test
    public void doWorkBean() throws Exception {
        doWorkBean.doWork();
    }
}
```

---

* 一个完整的@Bean注解包括 id,classes,initMethod,destoryMethod,ref和scope属性

```
    /**
     * 一个完整的bean配置包括了 id,class,initMethod,destroyMethod,·ref,scope
     *
     * @return
     */
    @Bean(initMethod = "init",destroyMethod = "destory")
    public DoWorkBean doWorkBean() {
        return new DoWorkBean();
    }
```



