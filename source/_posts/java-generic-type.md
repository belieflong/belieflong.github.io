---
title: Java泛型通配符之间的关系
date: 2017-05-06 17:22:33
categories:
	- Java
tags:
	- 学习总结
---
### 继承关系
``` java
class Apple{}
class Banana extend Apple{}
class Orange extend Apple{}
```
### 泛型里面
> A super B 表示A是B的父类或者祖先
A extend B 表示A是B的子类或者子孙

<!-- more -->

Java是单继承，所有继承的类构成一棵树。由于树这个结构上下是不对称的
- 参数写成：T<? super B>，对于这个泛型，?代表容器里的元素类型，由于只规定了元素必须是B的超类，导致元素没有明确统一的“根”（除了Object），所以这个泛型你其实无法使用它（除了把元素强制转成Object）。所以只能插入操作，而无法读
- 参数写成： T<? extends B>，由于指定了所有元素的“根”是B，你任何时候都可以安全的用B来使用容器里的元素，但是由于以B

> 为祖先的子树有很多，不同子树不兼容，所以禁止做插入操作，只做读取
