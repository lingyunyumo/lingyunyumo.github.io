---
layout:       post
title:        Python导入问题
tags:
    - Python
---

使用了`from __future__ import absolute_import`，出现此错误`ValueError: Attempted relative import in non-package`。

google之，http://blog.csdn.net/chinaren0001/article/details/7338041

	包含相对路径import 的python脚本不能直接运行，只能作为module被引用。原因正如手册中描述的，所谓相对路径其实就是相对于当前module的路径，但如果直接执行脚本，这个module的name就是“__main__”, 而不是module原来的name， 这样相对路径也就不是原来的相对路径了，导入就会失败，出现错误“ValueError: Attempted relative import in non-package”

相关的Python文档[PEP328](http://www.python.org/dev/peps/pep-0328/)。


