---
layout:       post
title:        制作web演示文稿
tags:
    - impress.js
    - MathJax
    - MathType
---

##概述

厌倦了PowePoint了么？

结合使用以下工具，可以制作漂亮的演示文稿：

* [impress.js](http://bartaz.github.io/impress.js): 这个javascript库可以用以制作炫丽的演示文稿。
* [MathJax](www.mathjax.org): 科学公式在网页上是显示是一大难题，有了它就释怀了。
* MathType: Word常用的公式编辑器，其可以导出为LaTex格式，方便的供MathJax使用。

注：impress.js需要现代浏览器的支持。推荐Chrome。

##使用impress.js

* 引入impress.js库。此库不依赖其它库！
* 实现参看作者的代码注释或者(此文)[http://www.cnblogs.com/fullhouse/archive/2012/04/24/2468940.html]

##使用MathJax

* 引入MathJax.js库，做可选的设置，就可以在Html文本中添加Tex等格式的公式代码了。
* 默认`[公式]`或者`(公式)`为行内公式`$$公式$$`为独占行公式。个人喜欢讲行内公式配置为`$公式$`。
* MathJax的包解压出来占100多M，主要是`fonts\HTML-CSS\TeX\png`几万个的小图片。这些图片是为了照顾
古老的浏览器的，删掉无妨。

##使用MathType

`选项->剪切和复制选项...`里选择 转化其它文字->Plain Tex，下面两个都不要勾选。然后就可以直接复制
MathType里的公式了，黏贴内容为Tex格式的文本（也就是MathJax可以直接使用的格式）。甚是方便。

##示例代码

打包好的在此：[web_presentation.rar](https://dl.dropboxusercontent.com/u/41623647/web_presentation.rar)

{% highlight html %}

<!doctype html>
<html>
<head>
  <meta http-equiv="content-language" content="zh-cn" />
  <meta http-equiv="content-type" content="text/html; charset=utf-8" />
  <title>Scientific Presentation Demo</title>
  <style type="text/css">
	body {
		font-family: 'PT Sans', sans-serif;
		min-height: 740px;

		background: rgb(215, 215, 215);
		background: -webkit-gradient(radial, 50% 50%, 0, 50% 50%, 500, from(rgb(240, 240, 240)), to(rgb(190, 190, 190)));
		background: -webkit-radial-gradient(rgb(240, 240, 240), rgb(190, 190, 190));
		background:    -moz-radial-gradient(rgb(240, 240, 240), rgb(190, 190, 190));
		background:     -ms-radial-gradient(rgb(240, 240, 240), rgb(190, 190, 190));
		background:      -o-radial-gradient(rgb(240, 240, 240), rgb(190, 190, 190));
		background:         radial-gradient(rgb(240, 240, 240), rgb(190, 190, 190));
	}

	.step {
		position: relative;
		width: 900px;
		padding: 40px;
		margin: 20px auto;

		-webkit-box-sizing: border-box;
		-moz-box-sizing:    border-box;
		-ms-box-sizing:     border-box;
		-o-box-sizing:      border-box;
		box-sizing:         border-box;

		font-family: 'PT Serif', georgia, serif;
		font-size: 48px;
		line-height: 1.5;
	}

	.slide{
		style="
		display: block;

		width: 900px;
		height: 700px;
		padding: 40px 60px;

		background-color: white;
		border: 1px solid rgba(0, 0, 0, .3);
		border-radius: 10px;
		box-shadow: 0 2px 6px rgba(0, 0, 0, .1);

		color: rgb(102, 102, 102);
		text-shadow: 0 2px 2px rgba(0, 0, 0, .1);

		font-family: 'Open Sans', Arial, sans-serif;
		font-size: 30px;
		line-height: 36px;
		letter-spacing: -1px;"
	}
	
	.slide q {
		display: block;
		font-size: 50px;
		line-height: 72px;

		margin-top: 100px;
	}

	.slide q strong {
		white-space: nowrap;
	}
  </style>
</head>
<body>
<div id="impress">
 
	<div class="step slide" data-x="0" data-y="0">
		<h2>使用 空格 或 左右键 浏览。</h2>
		
		This is my first slide
		这是行内公式：$\sum\limits_a^b {(a + \root 3 \of {b} )} $
		$$\sum\limits_a^b {(a + \root 3 \of {b} )} $$
	</div>

	<div class="step slide" data-x="1000" data-y="0">
		This is slide 2
	</div>
	 
	<div class="step slide" data-x="1000" data-y="-800">
		This is slide 3
	</div>

	<div class="step" data-x="1000" data-y="-1600" data-scale="0.5">
		This is slide 4
	</div>

	<div class="step" data-x="0" data-y="-1600" data-rotate="90">
		This is slide 5 and it rotates in.
	</div>

	<div class="step" data-x="-2600" data-y="-800" data-rotate-x="30" data-rotate-y="-60" data-rotate-z="90" data-scale="4">
	    This is slide 7 and it has a 3D transition AND a scale.
	</div>

	<div class="step" data-x="-3000" data-y="0" data-scale="10">
	    Overview
	</div>
</div>

<!-- javascript -->
<script type="text/javascript" src="impress.js"></script>
<script language="javascript">
  impress().init();
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    jax: ["input/TeX","output/HTML-CSS"],
	tex2jax: {
	  inlineMath: [['$','$']] //将行内公式配置为用$包裹，与行独占公式用$$包裹风格统一。
	}
  });
</script>
<!--script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script-->
<script type="text/javascript" src="MathJax-2.2/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
</body>
</html>

{% endhighlight %}
