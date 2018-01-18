---
layout:     post
title:      "kotlin之扩展函数"
subtitle:   "给别人的类添加方法"
date:       2018-01-18　16:21:04
author:     "Obaw"
catalog:    true
header-img: "img/post-kotlin-extensions.jpg"
tags:
    - Java
    - Kotlin
address:    么么直播
---

## 前言
以前使用java编码的时候，经常会发生这些情况，如

  - 为集合写某个方法
  - 把Json字符串转换成某个对象
  - 把某个对象转换成Json字符串

然后为了做的通用点就会去写一些工具类什么的，这样做的一个弊端就是每次我还的去找这个工具类是什么，直到今天了解到Kotlin的扩展函数。

## 实践
#### 编写扩展函数
增加ExtendUtils.kt文件，做为以后的扩展函数类，目前增加两个方法：
- 为String类型添加convert方法，用于转换字符串为Object
- 为Object类型添加json方法，用于将对象转换为Json字符串

```Kotlin
package com.memeyule.spark.utils

import kotlin.reflect.KClass

fun <T : Any> String.convert(valueType: KClass<T>): T = JacksonUtils.readValue(this, valueType)

fun Any.json(): String = JacksonUtils.writeValueAsString(this)
```

#### 调用扩展函数
调用时可以直接通过该类型的对象点出来，事例：
```Kotlin
// str->obj
val json = """{"one":1,"two":2}"""
val obj = json.convert(Map::class)

// obj->str
json = obj.json()
```

详情：[kotlin官方文档](http://kotlinlang.org/docs/reference/extensions.html)
