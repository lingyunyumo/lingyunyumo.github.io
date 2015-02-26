---
layout:       post
title:        基于ATL的ActiveX控件
tags:
    - ATL
    - ActiveX
    - CAPICOM
---

要对CAPICOM二次封装，解决IE调用时的英文提示。

ATL的ActiveX控件开发：

[这个](http://www.cnblogs.com/13590/archive/2007/08/01/838677.html)很有参考价值。

生成时失败，提示注册表权限问题。其实是所在磁盘时FAT32格式的原因。

1. 微软的解决方案：在“属性->配置属性->清单工具->常规“下有一个”使用FAT32解决办法，设置为"是"

2. 找到你的工程的文件夹，如（myproject），找到其下的myproject\myproject\Debug\，Delete it.