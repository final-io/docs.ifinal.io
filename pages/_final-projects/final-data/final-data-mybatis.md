---
formatterOff: "@formatter:off"
title: final-data-mybatis 
subtitle: final-data-mybatis 
summary: final-data-mybatis
categories: [] 
tags: [] 
date: 2022-03-04 16:42:55 +800 
version: 1.0
formatterOn: "@formatter:on"
---

# final-data-mybatis

## 概述

`final-data-mybaits`基于Spring和Mybatis开源框架，封装了简单的、通用的CRUD方法。

## 特性

### 自增的版本号

对于包含了被`@Version`注解的实体属性，在使用内置的更新方法时，会自动插入更新版本号的SQL片段`version = version + 1`。


### 增强的类型映射

框架加强了对于**枚举**和**Json**的类型映射。

#### 枚举

对于实现了`IEnum`的枚举类型，使用`getCode()`的值进行持久化，开发者可以直接使用具体的枚举类型进行接收。



#### Json

对于支持Json数据类型的数据库（如MySql 5.7+）而言，使用Json来存储一些数据会让业务扩展起来更方便，在默认情况下，实体对象只能使用String
类型来接收Json类型的数据，然后再显示的调用Json反序列化将Json转换化具体的实体类型，这是一项繁琐且无用的重复工作。

现在，对于Json的数据类型，可以在实体对象模型对应的属性上声明`@Json`注解，并将属性的类型定义为`json`数据真实的结构即可。

