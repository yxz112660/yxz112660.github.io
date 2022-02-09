---
title: MongoDB常用语法
author: YXZ
avatar: https://cdn.jsdelivr.net/gh/honjun/cdn@1.6/img/custom/avatar.jpg
authorLink: https://yxz112660.github.io/
authorAbout: 努力过好每一天
authorDesc: 努力过好每一天
categories: 技术
date: 2022-02-09 16:00:00
comments: true
tags: 
 - mongodb
 - 悦读
keywords: mongodb
description: 一些常用到的MongoDB技巧
photos: https://static.2heng.xin/wp-content/uploads//2019/02/wallhaven-672007-1-1024x576.png
---

## 查询
sql效果

字段1=条件1,

开始值<=字段2<=结束值,

字段3!=条件3,

字段4!=字段5,

字段6包含在[值1,值2,值3]中,

字段7不包含在[值1,值2,值3]中,

字段8数组长度等于值1,

正则匹配字段9以B开头的数据,

```mongodb
db.getCollection('表名A').find({
    "字段1":"条件1",
    "字段2":{
        "$gte":"开始值",
        "$lte":"结束值"
        },
    "字段3":{
        "$ne":"条件3"
        },
    $where:"this.字段4!=this.字段5",
    "字段6":{
        "$in":[值1,值2,值3]
        },
    "字段7":{
        "$nin":[值1,值2,值3]
        },
    "字段8": {
        "$size": 值1
        },
    "字段9": {
        "$regex": /^B.*/},
})
```
## 删除
注意:删除数据请先按条件查询再确定删除
```mongodb
db.getCollection('表名A').remove({
})
```

## 创建索引
多字段创建索引 1升序 -1降序
```mongodb
db.表名.createIndex({"字段1":1,"字段2":-1})
```

## 设置数据过期时间
根据某个ISODate(Date)类型字段设置索引数据过期时间,时长默认单位为秒
```mongodb
db.表名.createIndex({"字段1":1},{expireAfterSeconds:时长})
```