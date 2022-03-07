---
formatterOff: "@formatter:off"
title: 统一结果集
subtitle: response-body-advice 
summary: response-body-advice
categories: [] 
tags: [] 
date: 2022-03-05 16:38:04 +800 
version: 1.0
formatterOn: "@formatter:on"
---

# 统一结果集

被`@ResponseBody`标记的接口方法的返回值会进行统一的结果集封装。因此，业务开发者仅需要关心业务数据的处理，不需要再对数据进行额外的包装处理。


* HelloController

```java
package org.ifinalframework.demo;

@RestController
public class HelloController{
    @GetMapping("/hello")
    public String hello(){
        return "hello world!";
    }
}
```

* 结果

```json
{
  "status": 0,
  "description": "success",
  "code": "0",
  "message": "success",
  "data": "hello world!",
  "trace": "7aba435f-69d2-4c44-a944-315107623a92",
  "timestamp": 1605063263491,
  "duration": 0.063,
  "address": "127.0.0.1:80",
  "locale": "en",
  "timeZone": "Asia/Shanghai",
  "success": true
}
```