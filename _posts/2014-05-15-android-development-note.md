---
layout: post
title: "Android学习笔记"
tags: 
  - Android
  - Eclipse
---

## 前言

最近导师在做个电动汽车车载监测系统的项目，用户交互选定用Android平板了。

果然，事儿摊到我头上了。好吧，久违的 "Hello World!"，我来了。

## 准备

工欲善其事必先利其器。

### IDE&SDK

不用折腾，到Android Developer下载[ADT Bundle包](http://developer.android.com/sdk/index.html)，拿来即用的Eclipse环境。

    ADT: Android Developer Tools

打开Eclipse，通过File->New->Android Application Project按提示新建工程就是了。

### Android设备

我的电脑配置略低，尝试用ADT自带的虚拟设备未果，所以干脆用真机测试开发了。

吐槽下：台电的7寸4核平板，只要不到300RMB，电子设备真是越来越廉价啊。

真机调试首先要装驱动，不用折腾，装个豌豆荚，一切傻瓜自动。

还有，别忘了调整一下真机上调试相关的一些设置，什么“未知的源”、“调试模式”等。

## Hello World

首先，在开始动手前，必须了解下Activity这个重要的类，可以把它想成是“窗口”，类似于C#桌面程序开发中的Form类。所有，待会儿写代码时，跟GUI相关的类基本都是继承了Activity类的。

打开Eclipse，新的Android Application Project也建立好了。

你可以找到AndroidManifest.xml这个XML文件，是整个App的配置信息。在这里，你可以配置你的App的Android系统兼容范围、安装时所请求的权限等，但最重要的属<Application></Application>节点，以及其下的一个或多个<Activity></Activity>子节点。这些Activity子节点声明了我们源代码中继承了Activity类的类，让App知晓整个App所拥有的“窗口”的信息。特别容易遗忘的是：一心一意只顾着写code，当需要某个“窗口”在屏幕上显示时，程序崩溃了，但是检查代码十八遍也看不出头绪，最后暮然发现忘记在AndroidManifest.xml中声明Activity了！

res/layout/目录下是一些xml文件，每一个文件可以描述一个窗口的控件位置与样式。因此，Android开发中，GUI设计与业务逻辑是分离的（当然你也可以在.java源代码中编码设计GUI），即所谓的View与Model分离的设计理念。


src/目录下就是源代码所在，与一般的Java开发无异。

## 总结

写着写着顿悟到，再写些细节也无非是重复了其他人的类似文字。

所以，直接上总结了。

基本上，开发过程中一直在反复做着：

* 修改res/layout/目录下的GUI设计
* 修改src/目录下的业务逻辑相关代码
* 如果有新的“窗口”，去AndroidManifest.xml里声明新的Activity
