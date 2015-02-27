---
layout: post
title: "魔兽争霸3在英文系统下运行方法"
tags: 
  - 魔兽争霸
---

魔兽争霸3在英文系统下无法运行，提示“需要特定语言之windows”。

网上找了下，有两种方案。推荐方案二，对战平台适用。

我的系统：Windows 7 x64 英文企业版

###解决方案一

用UltraEdit修改游戏目录下game.dll文件，搜索3D04080000741B3D04，将74改成EB

此法直接运行魔兽可以，但是无法用于浩方、VS等对战平台。

###解决方案二（推荐）

修改注册表 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Nls\Language 下 Default 和 InstallLanguage， 由0409 改成 0804

如此修改后，windows开机时的文字会变成中文。魔兽争霸不再有任何运行问题。


