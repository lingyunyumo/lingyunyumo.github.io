---
layout:       post
title:        jekyll和markdown备忘之github pages
tags:         
    - Github
    - Jekyll
    - Markdown
---

##jekyll

* 文件头用一对`---`包裹起来的
* 代码高亮用仅需用类似`{% raw %}{% highlight python %}{% endraw %}`
和`{% raw %}{% endhighlight %}{% endraw %}`包裹。后台是pygments，需要引入必须的的CSS文件。
* 要高亮Lisp代码的话是`{% raw %}{% highlight cl %}{% endraw %}`，cl表示Common Lisp

另jekyll详细语法参考[这里](https://github.com/mojombo/jekyll/wiki/Liquid-Extensions)

##markdown

* 行前加几个`#`就表示Heading几
* 区块引用Blockquotes用`>`
* 无序列表用`*`或`+`或`-`
* 有序列表用`1.`式开头
* 行首缩进四空格表示`<pre><code>`块(基本不用，jekyll的highlight代替)
* 某行是三个以上的星号、减号，表示一个分隔线
* 行内式链接`This is [an example](http://example.com/ "Title") inline link.`
* 参考式链接`This is [an example] [id] reference-style link.`和`[id]: http://example.com/  "Optional Title Here"`
* `<em>`标签用`*`或`_`对代替
* `<strong>`标签用`**`或`__`对代替
* 行内代码用反引号`` ` ``包裹
* 图片`![Alt text](/path/to/img.jpg)`或`![Alt text](/path/to/img.jpg "Optional title")`。另也可如上面“参考式链接”的方式使用。
* 转义符为反斜线`\`，以下符号可转义

>* `\`   反斜线
>* `` ` ``   反引号
>* `*`   星号
>* `_`   底线
>* `{}`  花括号
>* `[]`  方括号
>* `()`  括弧
>* `#`   井字号
>* `+`   加号
>* `-`   减号
>* `.`   英文句点
>* `!`   惊叹号

另markdown详细语法参考[这里](http://wowubuntu.com/markdown/#editor)
[GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown)
