---
layout: post
title: "Python Challenge - 闯关学Python"
tags: 
  - Python
  - 游戏
published: true
---

今天无意家发现了个有趣的辅助学习Python的游戏——[Python Challenge](http://www.pythonchallenge.com/)。

总共33关，有些题实在得有柯南的脑力才能解开额>_<。

参考着官方答案思考动手一路下来，对Python的熟悉和理解绝对是大有裨益的，在此记录下闯关过程。

闯关代码放在Github上了。[这里](https://github.com/lingyunyumo/pythone-chanllenge-code)

##0

http://www.pythonchallenge.com/pc/def/0.html

2的38次幂 = 274877906944，进入下一关

##1

http://www.pythonchallenge.com/pc/def/274877906944.html

http://www.pythonchallenge.com/pc/def/map.html

有图上的3行提示，看出规律是右移2次。将一大段文本解密后告诉我们用同样的方法处理url。

即然map->ocr。

##2

http://www.pythonchallenge.com/pc/def/ocr.html

提示看源文件，一大堆乱字符，统计最少的字符。

结果为equality。

##3

http://www.pythonchallenge.com/pc/def/equality.html

根据提示，找寻的是这样的一些小写字母：他的左右各有三个大写字母包围着。

答案是linkedlist。

##4

http://www.pythonchallenge.com/pc/def/linkedlist.html

http://www.pythonchallenge.com/pc/def/linkedlist.php

点击网页上的图片之后，进入连接

http://www.pythonchallenge.com/pc/def/linkedlist.php?nothing=12345

提示and the next nothing is 92512，然后就把12345改成92512；他又提示and the next nothing is 64505……

意图很明显了，写个程序自动化如上动作。

##5

http://www.pythonchallenge.com/pc/def/peak.html

peak hell说要读出来，跟pickle的音很相似吧！banner.p是pickle.loads()的数据来源。loads()反序列化来的数据是二重序列，就是那种常见的纯文本来勾勒出图形的风格。

答案是channel。

##6

http://www.pythonchallenge.com/pc/def/channel.html

拉链(zip)安之zip压缩格式。下载channel.zip，然后写个程序提取注释什么的（看了官方的答案才明白，没用过zip库真不知道这么处理。。。）。

答案是oxygen。

##7

http://www.pythonchallenge.com/pc/def/oxygen.html

图片上的那条灰度条很可疑。最终是按照ASCII解码出来得到答案。我是官方解答的。。

答案是integrity

PS: Python没有内置图像处理库，推荐PI。

##8

http://www.pythonchallenge.com/pc/def/integrity.html

看源文件，最后的un和pw分别是用户名和密码的bz2加密。

解密后为huge和file。

##9

http://www.pythonchallenge.com/pc/return/good.html

提示：connect the dots

源文件里的first，second分别是两堆x和y的坐标，连起来以后first是一头牛，second是牛头。

如果才cow，提示说是公的。。。

答案是bull。

##10
http://www.pythonchallenge.com/pc/return/bull.html

http://www.pythonchallenge.com/pc/return/sequence.txt

a = [1, 11, 21, 1211, 111221,

len(a[30]) = ?

是不是感觉到了小学数奥和考公的意味儿~

官方的规律是这样的：

1

1个1，写作11

2个1，写作21

1个2，1个1，写作1211

……

答案是5808

##11

http://www.pythonchallenge.com/pc/return/5808.html

图片看起来像叠起来的，结合提示odd even，将此图提取为四张图：分别为奇奇，偶偶，奇偶，偶奇的像素。

看到某图中有上角的evil字样了吗？

##12

http://www.pythonchallenge.com/pc/return/evil.html

看源文件，图片名是evil1.jpg。

试试evil2.jpg，提示不是jpg是gfx，下载此文件。不知道做什么了。

试试evil3.jpg说是no more evil；不信，试试evil4.jpg，图片显示错误，其实它是文本文件，“Bert is evil”，下一题的提示。

看官方答案，图中那人把扑克牌分为5堆，提示把gfx文件分成5个文件，当然是按发牌的方式。。。

最后是5个图片，将图中的字母连起来得到disproportional

##13

http://www.pythonchallenge.com/pc/return/disproportional.html

call the evil,点击图片上的“5”，到达

http://www.pythonchallenge.com/pc/phonebook.php

竟然能从disproportional.html源文件里的remote字样猜到Remote Procedure Call（RPC）。。。

此RPC服务提供了一个“phone()”方法，还记得Bert is evil吗？

返回555-ITALY

##14

http://www.pythonchallenge.com/pc/return/italy.html

网页源码提示：100*100 = (100+99+99+98) + (...

把下面的小图按提示展开，得到一只猫。

使用cat，提示是uzi。

##15

http://www.pythonchallenge.com/pc/return/uzi.html

由右下角2月有29天确定是闰年，1XX6年是闰年，且结合源码中提示是第二年轻的，得知是1756年。

源码提示明天给他买花，得知是1756-01-27。百度or谷歌之，莫扎特。

答案mozart

##16

http://www.pythonchallenge.com/pc/return/mozart.html

对齐品红色的线段。这是gif图片，品红色在调色板里对应195。

调整后的图片显示答案romance

##17

http://www.pythonchallenge.com/pc/return/mozart.html

第四关的图片 + cookies = 查看第四关的cookies

第四关：http://www.pythonchallenge.com/pc/def/linkedlist.php

查看其cookies看到info = you+should+have+followed+busynothing...

从http://www.pythonchallenge.com/pc/def/linkedlist.php?busynothing=12345一路跟下去，
收集cookies里info的内容，得到BZh9.....这是bz2格式的数据，用bz2.decompress()解压得到如下提示

is it the 26th already? call his father and inform him that "the flowers are on their way". he'll understand.

Mozart's 的父亲是 Leopold，通过XML-RPC得到他的电话是555-VIOLIN。去violin.html得到提示no! i mean yes! but ../stuff/violin.php.

去http://www.pythonchallenge.com/pc/stuff/violin.php 告诉他"the flowers are on their way"（设置cookies中的info为此字符串）。

响应页面有句h well, don't you dare to forget the balloons.

##18

http://www.pythonchallenge.com/pc/return/balloons.html

找茬？别上当，是brightness！进入brightness.html，源码提示deltas.gz

解压后是个文本文件，十六进制的字符串，左右两大块（记事本不能执行换行符）。可以发现两块开头是
相同的（是png文件头），后面又有不同。结合"deltas"的意思，通过求最大公共子序，及左右两块分别
减去这个子序留下的内容，得到三个图片。一个图为下一关答案，另两个图为用户名和密码，后面关卡用的。

python内置了difflib库，方便的比较文本。

知识加油站：有两个字符串： a = "abcdefgh"，b = "123bcde4fhg5"， a和b的最大公共子序（顺序但
可不连续）为"bcdef"，最大公共子串为"bcde"（顺序并连续）。

用户butter密码fly

##19

http://www.pythonchallenge.com/pc/hex/bin.html

查看源文件，是一封email。附件是个wave音频(indian.wav)，听到"sorry"。去sorry.html提示- "what are you apologizing for?"。

将音频文件高地位调换，得到另一个音频文件(endian.wav)，听到"you are an idiot, aaaaaa~"。

答案idiot

##20

http://www.pythonchallenge.com/pc/hex/idiot.html

http://www.pythonchallenge.com/pc/hex/idiot2.html


图片说“私人财产，走远！”，下面位子又贱贱的让你小心刺探。。。发现图片的headers里响应
部分Content-Range: bytes 0-30202/2123456789（Chrome里只需按F12然后Networks里就可以方便地
查看headers）。原来只是返回了整个文件的前面一小段。

Range从30203开始发送请求，如此反复从上一个响应Content-Range的末尾接着新的请求，有如下返回：

Why don't you respect my privacy?

we can go on in this way for really long time.

stop this!

invader! invader!

ok, invader. you are inside now.

去invader.html，提示"Yes! that's you!"

瞎试探，试着请求从2123456789开始的Range，返回：

"esrever ni emankcin wen ruoy si drowssap eht"，倒过来"the password is your new nickname in reverse"

即invader倒过来 = redavni

从后往前刺探刺探，在2123456743处得到提示”and it is hiding at 1152983631“，这个位置藏着个Zip文件。

保存下来，用密码redavni解压，readme说这就是21关了！

##21

package.pack是个多重压缩的东东。readme里两句提示：

We used to play this game when we were kids  -- 老外小时候玩的游戏，文化的差别。

When I had no idea what to do, I looked backwards -- 适时逆序下

总之尝试zlib、bz2和逆序这三种操作，最后用这些操作序列对应空白、某符号和换行描出结果。

答案cooper

##22

http://www.pythonchallenge.com/pc/hex/copper.html

别忘了用户是butter密码是fly

源码提示 or maybe white.gif would be more bright

gif图片很容易想多多帧的，ImageSequence.Iterator(Image.open("white.gif"))得知133帧。

使用现代图像处理工具可以方便的查看每一帧的信息，可以发现每一帧上都有一个比其它点更黑的点。

把这些点的坐标找出来，最后描出结果。

答案bonus

##23

http://www.pythonchallenge.com/pc/hex/bonus.html

源码提示：what is this module? 无语，`import this`竟然会是一段文本，python的哲学。。

源码提示2：va gur snpr bs jung? 利用this模块`this.d.get()`解码，翻译过来 in the face of what?

The Zen of Python, by Tim Peters

[...] In the face of ambiguity, refuse the temptation to guess. [...]

答案ambiguity

#24

http://www.pythonchallenge.com/pc/hex/ambiguity.html

哟哟切克闹，迷宫！迷宫的入口与出口是在右上角与左下角。

解这个迷宫，得到一个zip压缩文件。其中又长图片。

答案lake

#25

http://www.pythonchallenge.com/pc/hex/lake.html

看网页源码，lake1.png附近有提示“can you see the waves?”。

不是图片中的波纹，而是lake1.wav ~ lake25.wav的声音文件。。。

用wave.open('lake1.wav','r').getnframes()返回是10800

每个碎片含有3600个像素的数据，将这25个碎片按5x5拼成一张图。

答案decent

#26

http://www.pythonchallenge.com/pc/hex/decent.html










