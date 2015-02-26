---
layout:       post
title:        学Python之(1.1)：基础恶补
tags:
    - Python
---

##节1.1的缘由

前面三课混乱无法进行下去。此版本1.1向传统方式的基础课致敬，但已经极简化。

##基本概念

###常量

* `5`、`1.23`、`9.25e-3`、`(-5+4j)`这样的数（整数、小数、科学计数法的数、复数）
* `'This is a string'`、`"It's a string!"`这样的字符串

###变量

* `a=5`、`b="Hello World!"`中的a和b都是变量
* 变量用来存储信息，并可以对存储的信息进行操作
* `i`、`__my_name`、`name_23`和`a1b2_c3`为合法的变量名（字母或下划线打头，非首字母可以是数字）
* `2things`（数字开头）、`this is spaced out`（有空格）和`my-name`（有"-"）为非法的变量名

###缩进

* 行首的空白用来决定行的缩进层次，从而用来决定语句的分组。
* 缩进在控制流（`if`、`for`、`while`）中体现得明显。

##运算符

###表1.1 运算符与它们的用法（引用[简明Python教程](http://sebug.net/paper/python/ch05s02.html)）

<table class="table">
    <tr>
        <th>运算符</th>
        <th>名称</th>
        <th>说明</th>
        <th>例子</th>
    </tr>
    <tr>
        <td>+</td>
        <td>加</td>
        <td>两个对象相加</td>
        <td>3 + 5得到8。'a' + 'b'得到'ab'。</td>
    </tr>
    <tr>
        <td>-</td>
        <td>减</td>
        <td>得到负数或是一个数减去另一个数</td>
        <td>-5.2得到一个负数。50 - 24得到26。</td>
    </tr>
    <tr>
        <td>*</td>
        <td>乘</td>
        <td>两个数相乘或是返回一个被重复若干次的字符串</td>
        <td>2 * 3得到6。'la' * 3得到'lalala'。</td>
    </tr>
    <tr>
        <td>**</td>
        <td>幂</td>
        <td>返回x的y次幂</td>
        <td>3 ** 4得到81（即3 * 3 * 3 * 3）</td>
    </tr>
    <tr>
        <td>/</td>
        <td>除</td>
        <td>x除以y</td>
        <td>4/3得到1（整数的除法得到整数结果）。4.0/3或4/3.0得到1.3333333333333333</td>
    </tr>
    <tr>
        <td>//</td>
        <td>取整除</td>
        <td>返回商的整数部分</td>
        <td>4 // 3.0得到1.0</td>
    </tr>
    <tr>
        <td>%</td>
        <td>取模</td>
        <td>返回除法的余数</td>
        <td>8%3得到2。-25.5%2.25得到1.5</td>
    </tr>
    <tr>
        <td><<</td>
        <td>左移</td>
        <td>把一个数的比特向左移一定数目（每个数在内存中都表示为比特或二进制数字，即0和1）</td>
        <td>2 << 2得到8。——2按比特表示为10</td>
    </tr>
    <tr>
        <td>>></td>
        <td>右移</td>
        <td>把一个数的比特向右移一定数目</td>
        <td>11 >> 1得到5。——11按比特表示为1011，向右移动1比特后得到101，即十进制的5。</td>
    </tr>
    <tr>
        <td>&</td>
        <td>按位与</td>
        <td>数的按位与</td>
        <td>5 & 3得到1。</td>
    </tr>
    <tr>
        <td>|</td>
        <td>按位或</td>
        <td>数的按位或</td>
        <td>5 | 3得到7。</td>
    </tr>
    <tr>
        <td>^</td>
        <td>按位异或</td>
        <td>数的按位异或</td>
        <td>5 ^ 3得到6</td>
    </tr>
    <tr>
        <td>~</td>
        <td>按位翻转</td>
        <td>x的按位翻转是-(x+1)</td>
        <td>~5得到6。</td>
    </tr>
    <tr>
        <td><</td>
        <td>小于</td>
        <td>返回x是否小于y。所有比较运算符返回1表示真，返回0表示假。这分别与特殊的变量True和False等价。注意，这些变量名的大写。</td>
        <td>5 < 3返回0（即False）而3 < 5返回1（即True）。比较可以被任意连接：3 < 5 < 7返回True。</td>
    </tr>
    <tr>
        <td>></td>
        <td>大于</td>
        <td>返回x是否大于y</td>
        <td>5 > 3返回True。如果两个操作数都是数字，它们首先被转换为一个共同的类型。否则，它总是返回False。</td>
    </tr>
    <tr>
        <td><=</td>
        <td>小于等于</td>
        <td>返回x是否小于等于y</td>
        <td>x = 3; y = 6; x <= y返回True。</td>
    </tr>
    <tr>
        <td>>=</td>
        <td>大于等于</td>
        <td>返回x是否大于等于y</td>
        <td>x = 4; y = 3; x >= y返回True。</td>
    </tr>
    <tr>
        <td>==</td>
        <td>等于</td>
        <td>比较对象是否相等</td>
        <td>x = 2; y = 2; x == y返回True。x = 'str'; y = 'stR'; x == y返回False。x = 'str'; y = 'str'; x == y返回True。</td>
    </tr>
    <tr>
        <td>!=</td>
        <td>不等于</td>
        <td>比较两个对象是否不相等</td>
        <td>x = 2; y = 3; x != y返回True。</td>
    </tr>
    <tr>
        <td>not</td>
        <td>布尔“非”</td>
        <td>如果x为True，返回False。如果x为False，它返回True。</td>
        <td>x = True; not x返回False。</td>
    </tr>
    <tr>
        <td>and</td>
        <td>布尔“与”</td>
        <td>如果x为False，x and y返回False，否则它返回y的计算值。</td>
        <td>x = False; y = True; x and y，由于x是False，返回False。在这里，Python不会计算y，因为它知道这个表达式的值肯定是False（因为x是False）。这个现象称为短路计算。</td>
    </tr>
    <tr>
        <td>or</td>
        <td>布尔“或”</td>
        <td>如果x是True，它返回True，否则它返回y的计算值。</td>
        <td>x = True; y = False; x or y返回True。短路计算在这里也适用。</td>
    </tr>
</table>

##控制流

如果没有控制流，那么程序只能按照代码的书写顺序一行一行的执行下来。这样的程序实在是太傻太天真了。

###if语句

####只是`if`

{% highlight python %}
print("‘爱’用英文怎么说：")
word = input()
if word == "love":
    print("你猜对了！")
{% endhighlight %}

####if和else

{% highlight python %}
goal = 'a'
print("现在我心中想好了a和b之一，你猜猜：")
guess = input()
if guess == goal:
    print("你猜对了！")
else:
    print("你猜错了！")
{% endhighlight %}

####if和elif和else

{% highlight python %}
goal = 23
print("现在我心中想好了一个1到100的数字，你猜猜：")
guess = int(input())
if n > goal:
    print("大了：")
elif n < goal:
    print("小了：")
else:
    print("被你蒙到了。。侥幸侥幸")
{% endhighlight %}

###while语句

{% highlight python %}
goal = 23
running = True
while running:
    guess = int(input('输入一个整数：'))

    if guess == goal:
        print("祝贺，你猜对了!") 
        running = False # 这句使while循环停止
    elif guess < goal:
        print("不对，再大点。") 
    else:
        print("不对，再小点。")
{% endhighlight %}

###for语句

{% highlight python %}
for i in range(0, 5):
    print(i)
{% endhighlight %}

输出是0到4的5个数字。

##break语句

{% highlight python %}
while True:
    s = input('输入一些内容：')
    if s == 'quit':
        break
    print(len(s))
{% endhighlight %}

* 上面的程序只有输入的是quit时才会结束，否则总是给出输入的字符串的长度。
* break语句也可以在for循环中使用。

###continue语句

{% highlight python %}
while True:
    s = input('输入一些内容：')
    if s == 'quit':
        break
    if len(s) < 3:
        continue
    print("嗨，你快乐吗？")
{% endhighlight %}

* 上面的程序只有输入的是quit时才会结束，否则总是给出输入的字符串的长度。
* 没输入一些内容回车后，会打印"嗨，你快乐吗？"，不过输入的内容的长度小于3时则不会打印此
  字符串（continue语句使忽略了此次循环中的剩余代码，直接开始下一次循环）。
* continue语句也可以在for循环中使用。

###今天到此结束

没错，今天到此结束。