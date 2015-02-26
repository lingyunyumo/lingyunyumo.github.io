---
layout:       post
title:        ICEM CFD笔记
tags:
    - ICEM CFD
---

##前言

这是我的ICEM CFD使用笔记，没有大的篇幅，没有书本式的章节，没有面面俱到的介绍，只有
过程中直接与使用相关的记录，为自己的遗忘准备的料。如果能为他人提供些许的参考，那么
最好不过。

ICEM CFD版本为12.0.1。

##几何

ICEM CFD提供了一定的几何建模能力，比之Gambit是先进得多。我现在几乎不用ICEM CFD自带
的几何工具（学习测试时图换其它软件麻烦，模型也简单时会用一下），而是使用一开始比较反感的
Solidworks（个人比较反感一切巨无霸软件而已）。

###自带几何工具

![toolbar geometry](\images\2012-10-09-cfd-icemcfd\toolbar-geometry.jpg)

ICEM CFD自带几何工具位于工具栏中“Geometry”标签下，其下前4个图标分别是点、线、面、体，
大部分命令可以想当然的使用，稍花点时间尝试便可。

###关于Solidworks：导入，Parts，重建拓扑。

Solidworks中做完几何后导出为igs格式，ICEM CFD中file->import geometry...便可。

导入完成后，你看到的模型只是“看到的”。所有的点线面都以自己的名字存在，没有组织（其实
是全部归于一个默认的叫做GEOM的Part）。要做的工作如下：

1. 左侧树状菜单:`Model->Parts`右键`Create Part`，按需修改`Part`名，点鼠标状的
`Select entitles`按钮，然后在几何上选择需要的元素，最后中键确定。
2. 重复步骤1，直到合理的将几何模型组织成多个`Part`为止。
3. `Geometry`工具栏，删除模型内的点和线。选择点或线元素式可以使用快捷键`a`选中所有。
4. `Geometry`工具栏第6个，注意`Tolerance`的大小，点击`Apply`重建拓扑结构。

##入门级网格划分

`Mesh`标签位于`Geometry`标签右侧。

下面是简单的但可用的的网格划分步骤：

* 第一个按钮：`Group Mesh Setup`，点击后左下脚子菜单关键地方是`Max element`。需要
经验，结合下侧的`Display`可以在主窗口直观到看到所设置的值对应多大的元素。
* 第二个按钮：`Part Mesh Setup`，点击后可以看到之前建的`Parts`一条条的罗列在此。这
时就是检验你的`Parts`建的合理否的时候了，一般将最关注的`Part`的`Max size`设置的小一些。
* 倒数第一个按钮：`Compute Mesh`，点击后左下脚子菜单，第二个`Volume Mesh`（2D模型的
话就第一个`Surface Mesh Only`），`Compute`。

网格已经划分好了，然后到`Output`标签下（不是在`Mesh`标签旁边，往右边找）。

* 第一个按钮：`Select solver`，两个下拉菜单，比如可以选择`Fluent_V6`和`ANSYS`。
* 第二个按钮：设置边界条件的，也可以之后到Fluent里去设置。
* 第四个按钮：导出网格文件。

##ICEM CFD精髓：Blocking

ICEM CFD的精髓亦是难点就是`Blocking`了（在`Mesh`标签右侧）。

Blocking具体方法网上资料挺多。

混合网格注意：有时候既需要四面体网格又需要六面体网格（3D实例）。六面体网格的生成是基于Blocking的，四面体网格
的生成是基于Body的。交界面的边界条件需要在ICEM里设置为interior（默认为interface），Fluent里无法修改。
