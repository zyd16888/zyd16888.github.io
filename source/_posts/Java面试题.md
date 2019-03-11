---
title: Java面试题（持续更新）
copyright: false
abbrlink: d2fd1f13
notshow: false
tags:
  - Java
categories: Java
description: 不断的重复造轮子······
sticky:
date: 2019-02-01 22:45:00
password:
image:
- "https://data.singlelovely.cn/CoverPicture/d2fd1f13.jpg!CoverPicture"
photos:
---

## 为什么集合类没有实现Cloneable和Serializable接口？

>克隆(cloning)或者是序列化(serialization)的语义和含义是跟具体的实现相关的。因此，应该由集合类的具体实现来决定如何被克隆或者是序列化。

实现Serializable序列化的作用

- 将对象的状态保存在存储媒体中以- 便可以在以后重写创建出完全相同的副本；
- 按值将对象从一个从一个应用程序域发向另一个应用程序域。

实现 Serializable接口的作用就是可以把对象存到字节流，然后可以恢复。所以你想如果你的对象没有序列化，怎么才能进行网络传输呢？要网络传输就得转为字节流，所以在分布式应用中，你就得实现序列化。如果你不需要分布式应用，那就没必要实现实现序列化。

## 什么是迭代器(Iterator)？

Iterator接口提供了很多对集合元素进行迭代的方法。每一个集合类都包含了可以返回迭代器实例的迭代方法。迭代器可以在迭代的过程中删除底层集合的元素,但是不可以直接调用集合的remove(Object Obj)删除，可以通过迭代器的remove()方法删除。

