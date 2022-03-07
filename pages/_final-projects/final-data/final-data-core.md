---
formatterOff: "@formatter:off"
title: final-data-core 
subtitle: final-data-core 
summary: final-data-core
categories: [] 
tags: [] 
date: 2022-03-07 21:39:11 +800 
version: 1.0
formatterOn: "@formatter:on"
---

# final-data-core

## Repository

`Repository`提供了大量CRUD常用的方法。

## 参数说明

|     参数      | 说明                                          |
|:-----------:|:--------------------------------------------|
|   `table`   | 表名，适用于实体模型与数据表一对多的场景，如分表                    |
|   `view`    | 视图，适用于不同业务场景下，操作不同数据表的场景                    |
|  `ignore`   | 忽略，适用于INSERT时是否忽略重复数据，即`INSERT IGNORE INTO` |
|   `list`    | 实体列表，适用于向数据表中插入数据的场景                        |
| `selective` | 可选择的，适用于更新场景下，只更新非空的数据列                     |
|  `update`   | 更新数据集合，适用于更新场景                              |
|  `entity`   | 实体数据，适用于更新场景                                |
|    `id`     | ID，适用于通过ID查询单个数据                            |
|    `ids`    | ID集合，适用于通过ID删除、更新、查询场景                      |
|   `query`   | 条件对象，适用于删除、更新、查询场景                          |


### Insert

`insert()`方法提供向数据表中插入数据的功能。

```java
insert([table,][view,][ignore,]list)
```


**参数与方法**

|             | `insert()` | `replace()` | `save()` | `delete()` | `update()` | `select()` | `selectOne()` | `selectIds()` |
|:-----------:|:----------:|:-----------:|:--------:|:----------:|:----------:|:----------:|:-------------:|:-------------:|
|   `table`   |     可选     |     可选      |    可选    |     可选     |     可选     |     可选     |      可选       |      可选       |
|   `view`    |     可选     |     可选      |    可选    |     -      |     可选     |     可选     |      可选       |       -       |
|  `ignore`   |     可选     |      -      |    -     |     -      |     -      |     -      |       -       |       -       |
| `selective` |     -      |      -      |    -     |     -      |     可选     |     -      |       -       |       -       |
|   `list`    |     非空     |     非空      |    非空    |     -      |     -      |     -      |       -       |       -       |
|  `update`   |     -      |      -      |    -     |     -      |     可选     |     -      |       -       |       -       |
|  `entity`   |     -      |      -      |    -     |     -      |     可选     |     -      |       -       |       -       |
|    `id`     |     -      |      -      |    -     |     -      |     -      |     -      |      可选       |       -       |
|    `ids`    |     -      |      -      |    -     |     可选     |     可选     |     可选     |       -       |      可选       |
|   `query`   |     -      |      -      |    -     |     可选     |     可选     |     可选     |      可选       |      可选       |

