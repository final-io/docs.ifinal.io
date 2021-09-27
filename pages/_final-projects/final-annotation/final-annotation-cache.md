---
formatterOff: "@formatter:off"
title: final-annotation-cache 
subtitle: final-annotation-cache 
summary: final-annotation-cache
categories: [] 
tags: [] 
date: 2021-09-27 13:59:42 +800 
version: 1.0
formatterOn: "@formatter:on"
---

# final-annotation-cache

Final Annotation Cache 基于Spring AOP，定义了常用的切面缓存注解。


## Annotations

### \@Cacheable

`@Cacheable`注解实现优先从缓存中获取数据，如果获取不到再调用业务方法查询数据，最后将查询到数据放置到缓存中去。

**用法：** 直接在目标方法上声明`@Cacheable`注解，并指定缓存有`key`和`field（可选）`。

```java
public interface UserService{
    
    @Cacheable(key="#{#id}")
    User findById(Long id);

}
```