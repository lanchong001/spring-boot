## Spring Boot Cache 的使用

---

### Spring Cache

Spring Cache 是 Spring 针对 Spring 应用给出的一整套缓存解决方案

Spring Cache 本身不提供缓存实现,而是通过统一的口径和代码规范,配置,注解等使你可以在Spring应用中使用各种Cache,而不用关心具体细节

---

### Spring Cache 接口

Sping 中关于缓存的定义，包括在接口 org.springframework.cache.Cache 中,它主要提供了如下方法

```
<T> T get(Object key, Class<T> type)
// 将指定的值，根据相应的key，保存到缓存中
void put(Object key, Object value);
// 根据键，回收指定的值
void evict(Object key)
```

---

### Cache Manager

Spring 提供了org.springframework.cache.CacheManager用来管理各种Cache,该接口只包含两个方法

```
// 根据名字获取对应主题的缓存
Cache getCache(String name);
// 获取所有主题的缓存
Collection<String> getCacheNames();
```

---

### 基于注解的缓存

Spring 提供了一系列的注解，包括@Cacheable，@CachePut，@CacheEvict等一系列注解来简化我们对缓存的操做，这些注解都位于org.springframework.cache.annotation包下。

```
//启用缓存配置(Spring Boot 启动类上配置)
@EnableCaching 

//指定某个方法的返回值是可以缓存的。在注解属性中指定缓存规则。
@Cacheable

//将方法的返回值缓存到指定的key中
@CachePut

//删除指定的缓存数据
@CacheEvict

//@Cacheable和@Cacheput都会将方法的执行结果按指定的key放到缓存中
//@Cacheable在执行时，会先检测缓存中是否有数据存在，如果有，直接从缓存中读取。如果没有，执行方法，将返回值放入缓存.
//@Cacheput会先执行方法，然后再将执行结果写入缓存。
```

---

[https://www.jianshu.com/p/fc076b6c2a13](https://www.jianshu.com/p/fc076b6c2a13)

[https://www.jianshu.com/p/3fbd5af2d789](https://www.jianshu.com/p/3fbd5af2d789)

[http://www.cnblogs.com/yueshutong/p/9381540.html](http://www.cnblogs.com/yueshutong/p/9381540.html)

