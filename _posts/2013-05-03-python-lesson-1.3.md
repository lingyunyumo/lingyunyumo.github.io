---
layout:       post
title:        学Python之(1.3)：数据结构
tags:
    - Python
---

##数据结构

###数据结构是什么

请看：列表、元组、字典！

###列表

{% highlight python %}
mylist = ['apple', 'boy', 'cat', 'dog']#初始化元组，用方括号
print(mylist)

print(len(mylist))#获得列表的长度

for item in mylist:#列表可以用for循环
    print(item)

mylist.append('bigapple')#在末尾追加元素
print(mylist)

mylist.sort()#排列列表内的元素
print(mylist)

print(mylist[0])#后接方括号及内数字，索引元素

del mylist[0]#删除指定索引位置的元素
print(mylist)
{% endhighlight %}

输出：

    ['apple', 'boy', 'cat', 'dog']
    4
    apple
    boy
    cat
    dog
    ['apple', 'boy', 'cat', 'dog', 'bigapple']
    ['apple', 'bigapple', 'boy', 'cat', 'dog']
    apple
    ['bigapple', 'boy', 'cat', 'dog']

###元组

{% highlight python %}
room = ('desk', 'chair', 'bed', 'lamp')#初始化元组，用圆括号
print(room)
print(len(room))
print(room[0])
print('%s, %s, %s and %s in room' % room)
{% endhighlight %}

输出：

    ('desk', 'chair', 'bed', 'lamp')
    4
    desk
    desk, chair, bed and lamp in room

元组与列表类似，只是初始化后不能再修改。

另，注意最后一句`print('%s, %s, %s and %s in room' % room)`。元组的打印技巧，`%`操
作符后的元组可以替换前面字符串内的`%s`符号。

###字典

{% highlight python %}
names = { 'AILSA':'古德语，快乐的姑娘的意思。',
          'ANDY':'ANDREW的简写，被人形容为高高的，金发的，童心未泯的普通男子。',
          'CARINA':'亲爱的小东西!',
          'ANGUS':'ANGUS被视作行为怪异，惹麻烦的傻瓜。' }

if 'ANDY' in names:
    print('ANDY means %s' % names['ANDY'])
    
del names['ANDY']
if 'ANDY' in names:
    print("'ANDY' is deleted. This line will not be printed.")

for name,description in names.items():
    print('name:%s, description:%s' % (name, description))
{% endhighlight %}

输出：

    ANDY means ANDREW的简写，被人形容为高高的，金发的，童心未泯的普通男子。
    name:ANGUS, description:ANGUS被视作行为怪异，惹麻烦的傻瓜。
    name:AILSA, description:古德语，快乐的姑娘的意思。
    name:CARINA, description:亲爱的小东西!

* 字典的初始化用到了`{}`、`:`和`,`符号。
* 字典也适用于`for`循环，不过要使用类似于`names.items()`的语句。

###序列

前几课学的字符串，以及刚才学的列表和元组，都是序列。

序列可以索引或者切片。

{% highlight python %}
s = 'abcdefg'
print(s)
print(s[0])
print(s[-1])
print(s[1:3])
print(s[2:])
print(s[-1:1])
print(s[:])
{% endhighlight %}

输出：

    abcdefg
    a
    g
    bc
    cdefg
    bcdef
    abcdefg

* 使用方括号和数字可以方便的索引序列指定位置的某个元素
* 索引是从0开始的
* 索引-1表示最后一个元素，-2则是倒数第二个...
* 方括号内的数字与冒号的组合可以对序列切片
* 冒号左或者右的数字可以省略，等价于第一个与最后一个的索引位置