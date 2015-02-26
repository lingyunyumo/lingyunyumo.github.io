---
layout:   post
title:    Python点滴
tags: 
    - Python
---

##Python数据拟合

用到以下包：

* Matplotlib：作图工具包，语法与Matlab相似。
* NumPy：数学包，数组矩阵等。Python做计算的基础包之一。
* SciPy：科学包，依赖NumPy包。用Python做科学工作的好工具。

代码：

{% highlight python %}
# -*- coding: utf-8 -*-
import matplotlib as mpl
mpl.rcParams['font.sans-serif'] = ['SimHei'] #指定默认字体  
mpl.rcParams['axes.unicode_minus'] = False #解决保存图像时负号'-'显示为方块的问题

import numpy as np
from matplotlib import pyplot as plt
from scipy.optimize import leastsq

def func(x, p):
    """
    数据拟合所用的函数: a*x*x+b*x+c
    """
    a, b, c = p
    return a*x*x+b*x+c
 
def residuals(p, y, x):
    """
    实验数据x, y和拟合函数之间的差，p为拟合需要找到的系数
    """
    return y - func(x, p)

x = np.array([0, 0.2,   0.3,    0.4,    0.5,    0.6,    0.7,    1.0])
y = np.array([0, 2.215, 3.9312, 6.0550, 8.6917, 11.808, 15.414, 27.8])
y /= y[-1]
print(y)

p0 = [1, 1, 0] # 第一次猜测的函数拟合参数
 
# 调用leastsq进行数据拟合
# residuals为计算误差的函数
# p0为拟合参数的初始值
# args为需要拟合的实验数据
plsq = leastsq(residuals1, p0, args=(y, x))
print(plsq[0])

plt.xlabel('开度')
plt.ylabel('流量')
plt.xlim(0,1)
plt.ylim(0,1)
plt.plot([0,1],[0,1])
plt.plot(x, y, 'bo')

xx = np.linspace(0,1)
plt.plot(xx, func(xx, plsq[0]), 'r-')

plt.grid()
plt.show()
{% endhighlight %}

##异或和校验

{% highlight python %}
s = "GPGGA,085014.955,2839.2050,N,11549.5721,E,1,04,03.6,76.6,M,-6.2,M,,"
result = '';
for i in range(len(s)):
  if(i==0):
    result = ord(s[i])
  else:
    result ^= ord(s[i])

print(hex(result))

a, b = 0, 1
while b < 10:
    print(b)
    a, b = b, a+b
{% endhighlight %}

##八皇后（递归）

{% highlight python %}
# -*- coding: utf-8 -*-
ans_count = 0
N = 8
panel = [([0] * N) for i in range(N)]

def show_answer():
    print('Answer ' + str(ans_count))
    for i in range(N):
        for j in range(N):
            if panel[j][N-1-i]==0:
                print '-',
            else:
                print 'Q',
        print('\n')
        
def show_count():
    print(ans_count)

def judge(i, j):
    for p in range(i):
        if panel[p][j]==1:
            return False
    for q in range(min([i,j])):
        if panel[i-1-q][j-1-q]==1:
            return False
    for q in range(min([i,N-j-1])):
        if panel[i-1-q][j+1+q]==1:
            return False
    return True;

def backtrace(i):
    if i == N:
        global ans_count
        ans_count += 1
        show_answer()
        raw_input("Press Enter to continue: ")
    else:
        for j in range(N):
            if judge(i, j):
                panel[i][j] = 1
                backtrace(i+1)
                panel[i][j] = 0
 
backtrace(0)
{% endhighlight %}

##列出所有子集（递归）

{% highlight python %}
# -*- coding: utf-8 -*-
# 用递归求一个字符串的所有子集
def rec_subsets(soFar, rest):
    if not rest:
        print(soFar)
    else:
        rec_subsets(soFar + rest[0], rest[1:])
        rec_subsets(soFar, rest[1:])

def list_subsets(s):
    rec_subsets("", s)

list_subsets('abbd')
{% endhighlight %}

##利用正则表达式替换字符

{% highlight python %}
import re
s = 'hello world!'
r = re.sub('(.*el)(.+)(ld.*)', lambda m: m.group(1) + '000' + m.group(3), s)
print(r)
{% endhighlight %}

##分形图案（递归）

{% highlight python %}
# -*- coding: utf-8 -*-
import Image, ImageDraw, math

def draw_triangle(x, y, s):
    points = ((x,y),(x+s,y),(x+s/2,y+math.sqrt(0.75*s*s)),(x,y))
    points = [(math.floor(p[0]),math.floor(p[1])) for p in points]
    imd.line(points)

def draw_fractal(x, y, s):
    draw_triangle(x, y, s)
    if s>10:
        draw_fractal(x, y, s/2) # left
        draw_fractal(x+s/2, y, s/2) # top
        draw_fractal(x+s/4,y+math.sqrt(0.75*s*s)/2, s/2) # right
        
im = Image.new("RGB",(600, 600)) 
imd = ImageDraw.Draw(im)
draw_fractal(0, 0, 512)
im.show()
{% endhighlight %}

