---
layout:       post
title:        流体仿真Fluent备忘
tags:
    - 仿真
    - Fluent
---

课题需要，学习流体仿真软件Fluent，做下记录，以防遗忘。因为自学笔记，只记录自以为主要和核心的内容。

##一般仿真流程

###几何建模

就是画出要仿真的对象的样子。最初时用Gambit笨拙地画着简单的几何，后来用ICEM CFD的先进
些的几何工具，但终归这两个软件只是旧时代与新时代的网格划分软件，几何并非它们的特长。
如今一直用Solidworks完成几何的建模了。

###网格划分

Gambit或者ICEM CFD？依照新事物淘汰就事物的历史法则，用ICEM CFD。它的Block是精髓，将复杂的
几何体解刨成简单的几何块的集合，以块为单位分别划分网格。

###计算求解

初学习的时候一直用Fluent 6.3，后来用Fluent 12.0.1。版本6.3时最难受的莫过于各项设置都得到菜单
里一级一级的找，而版本12.0.1的左侧快捷界面使人舒服多了。

###后处理

一般用Fluent自带的便可，当然也用过更专注后处理的Tecplot。

##Fluent细说

###常规设置

1. 导入mesh，尺寸scale，check
2. Models设置，Viscous选Laminar（层流）或Standard k-e（湍流）
3. Materials设置，Fluid默认是air，Solid默认是aluminum
4. Boundary Conditions设置，进出口和壁面等
5. Solution Methods设置，默认是SIMPLE方法，可以改为SIMPLEC
6. Solution Controls设置，一般默认即可
7. Monitors设置，一般Surface Monitors添加自己关注的监视
8. Solution Initialization，计算初始化
9. Run Calculation，开始计算
10. Graphics and Animations，云图和流线等查看

###动网格

1. Solver设置中将Steady改为Transient
2. Dynamic Mesh设置中开启Smoothing和Remeshing
3. Smoothing中Spring Constant Factor改为0.01
4. Remeshing中Minimum Length Scale等设置适当值（参考Mesh Scale Info...）
5. UFD相关，Define->User Defined->Functions->Compiled里添加Source Files（如下面“UFD实例”），并Build
6. Dynamic Mesh设置中Dynamic Mesh Zones设置，Motion UDF/Profile中为第5步的成果
7. Calculation Activities中可设置动画
8. Run Calculation中不同于Steady的选项，Time Step Size足够小以防负网格

UDF实例（需保存为.c文件，并放在你的case相同目录下）：

{% highlight c %}
#include <stdio.h>
#include "udf.h"
DEFINE_CG_MOTION(wallmove,dt,cg_vel,cg_omega,time,dtime)
{
    if(time<=3)
       cg_vel[1]=-0.01;
    else
       cg_vel[1]=0.0;
}
{% endhighlight %}

PS：

* 最初可以先以Steady计算一会儿，然后再开启动网格
* 控制台输入`file write-bc a.bc`可以将设置写入到a.bc文件;
    控制台输入`file read-bc a.bc`可以将a.bc文件中保存的设置读入case，
    方便类似的工况的设置。