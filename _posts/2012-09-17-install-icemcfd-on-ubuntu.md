---
layout:       post
title:        Ubuntu上安装ICEM CFD
tags:
    - Ubuntu
    - ICEM CFD
---

##安装源
安装来源：TLF-SOFT-ANSYS.PRODUCTS.V11.SP1.LINUX-MAGNiTUDE.iso
下载略难找，我下载的地址是

>ed2k://|file|Tlf-Soft-Ansys Products v11 Sp1 Linux-Magnitude.iso|1669425152|EA765EDFB0C80F355BD0F946BFCF311F|/

整个安装过程大致参考[此文](http://forum.ubuntu.org.cn/viewtopic.php?t=156708)

##需要csh
需要csh才能运行，装上。

##字体问题
启动界面出现，然后出错 

    can't load font screen14, using variable
    Signal 11 caught!
    segmentation violation - exiting after doing an emergency save
    Exiting...
    
修复`sudo apt-get install xfonts-75dpi xfonts-100dpi`

##键盘无法输入问题
`sudo icemcfd`之前`export LANG=en_US`，否则键盘无法输入。


##破解
a110sp1_calc.exe是windows平台下生成license.dat的，诺linux下没装wine的话可以在任何其它windows系统下运行

1. 选择no
2. 输入目标机器名
3. 输入目标网卡物理地址（去掉中间的冒号）
