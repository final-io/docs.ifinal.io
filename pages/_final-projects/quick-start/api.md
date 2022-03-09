---
formatterOff: "@formatter:off"
title: 服务端开发
subtitle: 服务端开发
summary: 服务端开发
categories: [] 
tags: [] 
date: 2022-03-09 13:30:18 +800 
version: 1.0
formatterOn: "@formatter:on"
---



## 引入依赖

```xml
<dependency>
    <groupId>org.ifinalframework.boot</groupId>
    <artifactId>final-boot-starter-web</artifactId>
    <version>${latest.release.version}</version>
</dependency>
```

> 注意：请将 `${latest.release.version}` 更改为实际的版本号。



## 定义接口

```java
@SpringBootApplication
@RestController
public class DemoApplication {

	@GetMapping("/hello")
	public String hello() {
		return "hello world!";
    }
}
```



## 访问接口

```shell
curl http://localhost:8080/hello
```

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

> 注意：接口返回的数据由框架封装为统一的结果对象返回，开发者只需要返回核心业务数据。