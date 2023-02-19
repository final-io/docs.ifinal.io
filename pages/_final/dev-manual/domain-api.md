---
formatterOff: "@formatter:off"
title: 领域接口
subtitle: 对象关系映射
summary: 对象关系映射
categories: [] 
tags: [] 
date: 2022-03-08 13:30:18 +800 
version: 1.0
formatterOn: "@formatter:on"
---

# 领域接口



## 概述

通过资源标识符，Final内置了常用的接口来操作各种资源。

| 操作     | 方法     | path                               | 参数格式 | 参数            |
| -------- | -------- | ---------------------------------- | -------- | --------------- |
| 列表查询 | `GET`    | `/{prefix}/{resource}`             | `form`   |                 |
| 查询详情 | `GET`    | `/{prefix}/{resource}`             | `form`   |                 |
| 添加     | `POST`   | `/{prefix}/{resource}`             | `json`   |                 |
| 修改     | `PUT`    | `/{prefix}/{resource}/{id}`        | `json`   |                 |
| 修订     | `PATCH`  | `/{prefix}/{resource}/{id}`        | `json`   |                 |
| 修改YN   | `PATCH`  | `/{prefix}/{resource}/{id}/yn`     | `form`   | yn=1\|0         |
| 修改状态 | `PATCH`  | `/{prefix}/{resource}/{id}/status` | `form`   | status={status} |
| 删除     | `DELETE` | `/{prefix}/{resource}/{id}`        |          |                 |
|          |          |                                    |          |                 |

> * `prefix`：默认为`api`。



## 列表查询 GET /{prefix}/{resource}

通过访问`GET /{prefix}/{resource}`接口，开发者可以直接访问资源列表查询。
