---
layout:       post
title:        学Python之(0.1)：先睹为快
tags:
    - Python
---

大学时学的是国贸的张Amy要陶大头教她编程。陶大头稍微思索了下，按老套路教C或C++什么的真心木有意思。
正好自己也有兴趣把Python玩熟，然后就寓教于学的和张Amy一起开始了Python之旅。

写文记录:教学方式略去冗余的繁琐的内容，一切尽量以实用与有趣为准绳。

##预备

全程WindowsXP下使用Python3.3.1[点我下载](http://www.python.org/ftp/python/3.3.1/python-3.3.1.msi)，不考虑2.x兼容(_历史的马车滚滚向前_)。

* 安装完后：开始》程序》Python 3.3》IDLE(Python GUI)。这就是官方的编辑器了。
* 界面中的">>>"是命令提示符，适合输入一行运行一行代码。
* File》New Window。这里可以输入程序，然后按F5运行。

##源起Hello World!

Hello World！真乃学编程的优良传统也：

{% highlight python %}
print("Hello World!")
{% endhighlight %}

屏幕打印出`Hello World!`了吧！没错，就是这么简单!

* print的作用是显示紧跟其后的括号里的字符串(引号引起来的叫做字符串)，基本的人机交互功能之一。
* 另一基本的人机交互功能之一: `input()`。

{% highlight python %}
s = input("请输入你的姓名：")
print("你好" + s)
{% endhighlight %}

运行输入_Amy_回车，显示内容是_你好Amy_。上面代码里的`input()`等待用于的键盘输入(以回车
结束），把用户输入的内容放入变量s中(变量跟代数中的变量类似，用着就懂越解释越糊涂)供
以后用。`print("你好" + s)`就是我上句话说的”供以后用“。


PS：上面两行代码跟下面代码等价:

{% highlight python %}
print("请输入你的姓名：")
s = input()
print("你好" + s)
{% endhighlight %}

具体就不解释了，悟性有木有，试试就知道。

##回忆今天，期待明天

想想今天学了什么：

* `print()`：显示字符串。
* `input()`：等待用户输入，获得字符串。

你已经初触人机交互了，你可以跟计算机有问有答了!

##你暂所不及的一个程序

{% highlight python %}
goal = 23
print("现在我心中想好了一个1到100的数字，给你3次机会猜猜：")
for i in range(0,3):
    n = int(input())
    if n > goal:
        print("大了：")
    if n < goal:
        print("小了：")
    if n == goal:
        print("被你蒙到了。。侥幸侥幸")
print("按下回车退出程序咯")
input()
{% endhighlight %}

"23"是乔丹么？


    





