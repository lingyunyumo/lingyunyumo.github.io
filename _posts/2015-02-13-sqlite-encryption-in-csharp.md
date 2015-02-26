---
layout: post
title: "C#下SQLite加密"
tags: 
  - C#
  - SQLite
  - 加密
---

C#开发桌面程序，使用了SQLite3。问题来了，开源版的SQLite3没有实现加密功能。

baidu+bing+google了一圈，解决方案虽多，但没有满意的简单直接的方法。

正失望叹气之际，发现C#下竟有简洁的方法，可气的是眼皮底下一直没发现。

关键代码如下：

{% highlight csharp %}
// C#下的此程序集不仅做到了一个SQLite的Provider本分，还顺带了加解密功能
using System.Data.SQLite;

// 加密
SQLiteConnection conn = new SQLiteConnection("Data Source=test.db;Version=3;");
conn.Open();
conn.ChangePassword("1234");
conn.Close();

//解密
SQLiteConnection conn = new SQLiteConnection("Data Source=test.db;Version=3;Password=1234");
conn.Open();
conn.ChangePassword(string.Empty);
conn.Close();
{% endhighlight %}

注：加密后的数据库文件无法使用其他可视化工具打开。可以这么应对：开发时不加密；发布前加密，并将密码添到连接字符串。

