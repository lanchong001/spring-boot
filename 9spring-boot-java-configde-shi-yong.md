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

---

* SpringBootTest 单元测试中获取上下文,直接通过 @Autowired 注入相关上下文

```
@RunWith(SpringRunner.class)
@SpringBootTest(classes = Config.class)
public class ConfigTest {

    @Autowired
    public ApplicationContext context;

    @Test
    public void doWorkBean() throws Exception {
        DoWorkBean doWorkBean1 = context.getBean(DoWorkBean.class);
        System.out.println(doWorkBean1);
        DoWorkBean doWorkBean2 = context.getBean(DoWorkBean.class);
        System.out.println(doWorkBean2);
    }
}
```

---

### scope 的5种类型

1. singleton : 容器中创建时只存在一个实例,所有引用此bean都是单一实例.

2. prototype : spring容器在进行输出prototype的bean对象时,会每次都重新生成一个新的对象给请求方,虽然这种类型的对象的实例化以及属性设置等工作都是由容器负责的.但是只要准备完毕,并且对象实例返回给请求方之后,容器就不在拥有当前对象的引用,请求方需要自己负责当前对象后继生命周期的管理工作,包括该对象的销毁.

3. request : Spring容器，即XmlWebApplicationContext 会为每个HTTP请求创建一个全新的RequestPrecessor对象,当请求结束后,该对象的生命周期即告结束.

4. session : 对于web应用来说,放到session中最普遍的就是用户的登录信息.Spring容器会为每个独立的session创建属于自己的全新的实例.

5. globalsession : global session只有应用在基于porlet的web应用程序中才有意义,它映射到porlet的global范围的session,如果普通的servlet的web 应用中使用了这个scope,容器会把它作为普通的session的scope对待.

### 



