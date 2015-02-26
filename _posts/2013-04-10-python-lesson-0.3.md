---
layout:       post
title:        学Python之(0.3)：先睹为快
tags:
    - Python
---

##这次课将与之作战的“大家伙”

{% highlight python %}
dic = {} #定义了一个叫dic的字典变量，后面有用的
#我是一行注释，程序运行时完全被无视的注释就是我啊
#你应该也发现了，‘井号’以及其后的内容的就是注释了
txt = "I am a 我我是中国人人人人 chinese chine" #要处理的文本
for s in txt:
    if s not in dic:
        dic[s] = 1
    else:
        dic[s]+= 1
for k, v in dic.items():
    print(str(k) + "," + str(v))
#下面这一行长长的代码与上面的两行for循环代码是等价的，试着读懂吧
#print("\n".join('%s,%s' % (k, v) for k, v in dic.items()))
print("以这行可以用来查找一段文字中某个词出现的次数：")
print('有这么多个"人"字：' + str(txt.count("人")))
{% endhighlight %}

这一坨代码里有很多新知识哦。一眼看去乱糟糟天数没关系，看完下面的解说回过头来
还是云里雾里也是正常滴！再多看一遍再多想一点，还是不懂的话你我之间有一个可以
反省反省了。

##字典变量

第一行的`dic = {}`：等号右边是一对大括号，顾名思义字典变量如字典，此时还只是部
空字典了（大括号的什么都没有有）。如果在上面那堆代码最后加上`print(dic)`的话，会
多输出这些：
    
    {'国': 1, '人': 4, 's': 1, '中': 1, '我': 2, '是': 1, 'n': 2, 'm': 1, 'i': 2, 'I': 1, 'h': 2, 'e': 3, 'c': 2, 'a': 2, ' ': 5}

格式很容易理解吧。用法参考最上面的代码咯。

##注释

已经在代码段里以注释的方式解释了。

##单引号与双引号

分条举例：

* `s = "Let's go"`：文本内容里有单引号，那么就用双引号定义字符串
* `s = 'I realy like "python"!'`：文本内容里有双引号，那么就用单引号定义字符串
* 文本内容里既有双引号又有单引号呢？下回再听分解！

##“加等”运算符

`dic[s]+= 1`中出现了此运算符。下面的代码给有说明性：

{% highlight python %}
total = 0
for i in range(0,10):
    total += i
print(total)
{% endhighlight %}

输出是45（为什么不是55？回去补补课吧！提示`range(0,10)`）。`total += i`等价
于`total = total + i`。举一反三，自然还有“减等”、“乘等”、“除等”。

##缩进

你一定发现一个现象，Python代码这么多行，可是它们有的顶格，有的行前会有些空格，此为“缩进”。
“缩进”使得Python代码有了层次，还是用上面的例子（“代码拷过来撑下场面”）；

{% highlight python %}
total = 0
for i in range(0,10):
    total += i
print(total)
{% endhighlight %}

`for`循环只是循环了`total += i`，而没有循环`print(total)`这一行。如果把上面的代码修改成：

{% highlight python %}
total = 0
for i in range(0,10):
    total += i
    print(total)
{% endhighlight %}

输出就会变成很多很多（确切的是10行）了。领会了吧亲？

##陶大头已心中有数而没讲明的问题

1. 文本内容里既有双引号又有单引号呢？
2. 什么事有数？

##PS:::::::

今天把此站点的Jekyll生成路径规则修改了，而第三方评论系统的历史评论都挂名在就的网页路径
下了，所以除了[“关于About”页面](/about.html)的评论都一去不复返了555。
