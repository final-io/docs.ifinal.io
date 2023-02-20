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



## 查询

### GET /{prefix}/{resource}｜列表查询

通过访问`GET /{prefix}/{resource}`接口，开发者可以直接访问资源列表查询。

| SPI                        | 描述           |
| -------------------------- | -------------- |
| `PreQueryConsumer`         | 前置查询消费者 |
| `PostQueryConsumer`        | 后置查询消息者 |
| `AfterReturnQueryConsumer` | 返回查询消息者 |

### GET /{prefix}/{resource}/detail｜查询详情

通过访问`GET /{prefix}/{resource}/detail`接口，开发者可以直接访问资源详情。

| SPI                       | 描述               |
| ------------------------- | ------------------ |
| `PreDetailQueryConsumer`  | 前置查询详情消费者 |
| `PostDetailQueryConsumer` | 后置查询详情消息者 |
| `PostDetailConsumer`      | 返回查询详情消息者 |

### GET /{prefix}/{resource}/{id}｜查询详情

通过访问`GET /{prefix}/{resource}/{id}`接口，开发者可以直接访问资源详情。

| SPI                  | 描述               |
| -------------------- | ------------------ |
| `PostDetailConsumer` | 返回查询详情消息者 |



## 添加

### POST /{prefix}/{resource}｜添加（支持批量）

通过访问`POST /{prefix}/{resource}`接口，开发者可以直接创建资源。

| SPI                  | 描述 |
| -------------------- | ---- |
| `PreInsertFilter`    |      |
| `PreInsertConsumer`  |      |
| `PostInsertConsumer` |      |



## 修改

### PUT /{prefix}/{resource}｜修改



| SPI                  | 描述               |
| -------------------- | ------------------ |
| `PostDetailConsumer` | 返回查询详情消息者 |



### PUT /{preifx}/{resource}/{id}｜修改

| SPI                  | 描述               |
| -------------------- | ------------------ |
| `PostDetailConsumer` | 返回查询详情消息者 |



### PATCH /{prefix}/{resource}/{id}｜修改

| SPI                  | 描述               |
| -------------------- | ------------------ |
| `PostDetailConsumer` | 返回查询详情消息者 |



### PATCH /{prefix}/{resource}/{id}/yn｜修改YN

| SPI                  | 描述               |
| -------------------- | ------------------ |
| `PostDetailConsumer` | 返回查询详情消息者 |



### PATCH /{prefix}/{resource}/{id}/status｜修改状态

| SPI                  | 描述               |
| -------------------- | ------------------ |
| `PostDetailConsumer` | 返回查询详情消息者 |



## 删除

### DELETE /{prefix}/{resource}/{id}｜删除

| SPI                       | 描述 |
| ------------------------- | ---- |
| `PreDeleteQueryConsumer`  |      |
| `PreDeleteConsumer`       |      |
| `PostDeleteQueryConsumer` |      |
| `PostDeleteConsumer`      |      |



### DELETE /{prefix}/{resource}｜删除

| SPI                  | 描述 |
| -------------------- | ---- |
| `PreDeleteConsumer`  |      |
| `PostDeleteConsumer` |      |





