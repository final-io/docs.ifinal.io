---
formatterOff: "@formatter:off"
title: Final Web
subtitle: final-web 
summary: final-web
categories: [] 
tags: [] 
date: 2021-09-27 13:09:51 +800 
version: 1.0
formatterOn: "@formatter:on"
---

# Final Web

## 统一结果集封装

`final-web`对`@ResponseBody`结果进行统一的结果集封装，因此开发人员只需要关心核心业务数据即可，不再需要对结果集进行显示的封装。

## 全局异常处理

`final-web`还对业务层抛出的异常进行了全局异常处理，包含业务异常（`IException`）和程序异常，异常也会被封装成统一的结果集返回给调用方，以便调用方统一处理。