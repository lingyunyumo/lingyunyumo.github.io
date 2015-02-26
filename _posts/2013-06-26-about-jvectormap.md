---
layout: post
title: 关于jvectormap
tags: 
  - jquery
  - jvectormap
published: true
---

jvectormap是jquery的一个矢量地图插件。

* [官网](http://jvectormap.com/)提供了一些地图。不过中国地图没有台湾，自己修改了一下，
添加了台湾。
* 官网的地图中省份的命名看不出意义来，改成了汉语拼音。

修改后的文件在[这里](https://www.dropbox.com/sh/2lbclhwguqzrwlt/nGxBavSX0N/jquery-jvectormap-cn-mill-zh.js)。

注：写此文时所用的为jquery-jvectormap-1.2.2.min.js即jvectmap版本为1.2.2，其地图格式与网上许多文章中所用的早期jvectmap版本所用的不兼容。

相应的示例代码：

{% highlight html %}
<!DOCTYPE html>
<html>
<head>
    <title>jvectormap</title>
    <link href="jvectormap/jquery-jvectormap-1.2.2.css" media="screen" rel="stylesheet" type="text/css" />
	<script src="jquery/jquery-1.9.1.min.js" type="text/javascript"></script>
    <script src="jvectormap/jquery-jvectormap-1.2.2.min.js" type="text/javascript"></script>
    <script src="jvectormap/jquery-jvectormap-cn-mill-zh.js" type="text/javascript"></script>
	<script type="text/javascript">
	$(function(){
	var gdpData = {
        "Shanghai": 16.63,
        "Zhejiang": 11.58,
        "Anhui": 158.97,
        "Shanxi": 200.12, //山西
        "Shaanxi": 99.78 //陕西：英文中如此拼写，区别于山西
    };
    $('#map').vectorMap({
	  map: 'cn_mill_zh',
	  series: {
        regions: [{
          values: gdpData,
          scale: ['#C8EEFF', '#0071A4'],
          normalizeFunction: 'polynomial'
        }]
      },
      onRegionLabelShow: function(e, el, code){
        el.html(el.html()+' (GDP - '+gdpData[code]+')');
      }
    });
	});
    </script>
</head>
<body>
    <div id="map" style="width: 600px; height: 400px"></div>
</body>
</html>
{% endhighlight %}
