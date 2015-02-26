---
layout:       post
title:        BAE(Baidu App Engine)上的Python相关
tags:
    - BAE
    - Python
---

##git客户端

Baidu的git竟然可以用Github For Windows啊！舒心不是一点点。

1. 先把你在Baidu的库git clone下来。
2. 在Github For Windows中Add一个库，名字同你刚才git clone的库。
3. 把1中的库复制到2中的库目录。
4. 接下来就照常使用Github For Windows了。

##静态文件支持

百度的文档中对静态文件支持的配置有：

>handlers:
>  - url : /
>    script: index.py
>
>  - url : /(.*).py
>    script: $1.py
>
>  - url : /static/(.*)
>    script: /static/$1
>
>  - expire : .jpg modify 10 years
>  - expire : .swf modify 10 years
>  - expire : .png modify 10 years
>  - expire : .gif modify 10 years
>  - expire : .JPG modify 10 years
>  - expire : .ico modify 10 years

应该把

>  - url : /static/(.*)
>    script: /static/$1

放到前面