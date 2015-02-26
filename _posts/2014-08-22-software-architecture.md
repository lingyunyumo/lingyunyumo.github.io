---
layout: post
title: "软件架构"
tags: 
  - 架构
  - MVC
  - MVP
---

软件设计中充斥了各种模式：设计模式、构件模式、架构模式。。。概念令人混乱。

最近又试着去搞明白一些之前似懂非懂的相关知识。

## 重要概念：IOC和DI

* IOC：Inversion of Control 控制反转
* DI:Dependency Injection 依赖注入

两篇不错的博文：

* [关于IOC和DI的理解](http://www.cnblogs.com/niuniu1985/archive/2010/01/13/1646375.html)
* [架构师之路(39)---IoC框架](http://blog.csdn.net/wanghao72214/article/details/3969594)

## MVP

基于上面两个重要概念，写了一个[Demo - 19K](/misc/MVPExample.zip)：

* MVP模式（Model-View-Presenter）
* 实现加法和减法功能的计算器
* WinForm程序，VS2010和.Net Framework 4.0

参考了以下两篇文章及代码：

* [WinForms Model View Presenter](http://www.codeproject.com/Articles/14660/WinForms-Model-View-Presenter)
* [WinForms MVP - An MVP Framework for WinForms](http://www.codeproject.com/Articles/522809/WinForms-MVP-An-MVP-Framework-for-Winforms)







