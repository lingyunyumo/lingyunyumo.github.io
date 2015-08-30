---
layout: post
title: "Windows上搭建Shadowsocks服务器（Amazon的EC2）"
tags: 
  - Shadowsocks
  - EC2
---

1. 新加坡（或东京）的EC2虚拟机，Windows系统，公网IP配置好
2. EC2网页控制台，到Security Group开启以下端口
   1. 入站出站TCP的3389端口，用于RDP远程控制
   2. 入站出站TCP的1080和8388端口，Shadowsocks使用
   3. **入站TCP和UDP的8989端口**，费了好一会儿发现Shadowsocks还要用这端口
   4. 其它端口如80和443等
3. RDP到Windows系统，安装Python2.7
4. pip安装Shadowsocks，`pip install shadowsocks`
5. 创建`C:\shadowsocks.json`，文件内容见下方
6. 运行Shadowsocks服务，`ssserver -c C:\shadowsocks.json`

{% highlight json %}
{
    "server":"0.0.0.0",  // 服务器地址，就这么四个0就可以了
    "server_port":8388,
    "local_address": "127.0.0.0",
    "local_port":1080,
    "password":"yourpassowrd",  // 密码
    "timeout":600,
    "method":"table"  // 加密方法，windows下安装openssl等麻烦，使用table方法最简单
}
{% endhighlight %}







