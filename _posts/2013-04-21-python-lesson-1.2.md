---
layout:       post
title:        学Python之(1.2)：基础再多一点
tags:
    - Python
---

##函数

###函数是什么

基本上与数学中的函数概念类似。你只看到一个函数名，其实里面包含了一堆逻辑。

###函数之Hello World

{% highlight python %}
def sayHello():
    print('Hello World!')

sayHello() # 调用函数
{% endhighlight %}

* 前两行代码定义了一个叫“sayHello”的函数
* 第三行调用了上面定义的函数

###函数之参数

{% highlight python %}
def sayHelloToSomeone(name):
    print('Hello' + name)

sayHelloToSomeone('Amy') # 调用函数
{% endhighlight %}

* 定义函数的时候函数名后的括号里不再是空着了，里面的东西叫参数
* 调用有参数的函数时，可以把参数传递个函数（类比数学里的函数如f(x),你调用时可以使f(0),也
可以使f(99.5)）

###默认参数

{% highlight python %}
def sayHelloToSomeone(name='Amy'):
    print('Hello' + name)

sayHelloToSomeone() # 调用函数，括号里空着
sayHelloToSomeone('David')
{% endhighlight %}

* 注意定义函数时括号里的内容
* 调用函数时如果括号里是空的，则使用默认的'Amy'
* 调用函数时如果括号里不是空的，则使用给定的参数

###函数返回（return语句）

{% highlight python %}
def max(x, y):
    if x > y:
        return x
    else:
        return y

m = max(2, 3)
print(m)
{% endhighlight %}

* 函数内的`return`语句可以可以将内容返回个函数调用者
* `return`还意味着函数到此结束了
* `m = max(2, 3)`语句使`m`的值变成了`3`

##模块

###什么是模块

函数是对代码的一次“重用”，那么可以认为是模块是很多函数的集合（其实还有其它的内容如
某些变量）。
现在我们先不学习怎么设计自己的模块，我们先学习Python自带的标准库模块。

###sys模块

{% highlight python %}
import sys # 这句导入我们想用的模块，只有先导入才可以使用

print(sys.path)
{% endhighlight %}

* sys模块包含了与Python和它的环境有关的参数和函数
* `print(sys.path)`在屏幕上打印Python的环境相关路径

###os模块

{% highlight python %}
import os

cwd = os.getcwd()
print(cwd)
{% endhighlight %}

* os模块包含了与操作系统相关的一些参数和函数
* `os.getcwd()`函数取得当前

###写个自己的模块吧

{% highlight python %}
def sayHello():
    print('Hello，你好啊')

version = '0.1'
{% endhighlight %}

将上面的代码保存为mymodle.py文件。

{% highlight python %}
import mymodle
mymodle.sayHello()
{% endhighlight %}

* 用如上代码调用mymodle（不用.py后缀）
* 如果失败的话，可能是没有将mymodle.py文件放在同目录下(其实放在sys.path中的任一目录下
都可以的)
* 多个相关的模块可以按目录组成成包，记住每个文件夹下创建一个`__init__.py`文件！

##休息下

今天到这儿了，休息去了。