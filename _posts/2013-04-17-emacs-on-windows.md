---
layout:       post
title:        Emacs相关
tags:
    - Emacs
    - Windows
---

##Windows版的前序工作

* 到[这里](http://ftp.gnu.org/pub/gnu/emacs/windows/)可以下载到Emacs的windows版本
* 双击bin文件夹里的addpm.exe进行安装，安装后将在开始菜单生成Gnu Emacs/Emacs链接
* 打开注册表，找到`HKEY_LOCAL_MACHINE/SOFTWARE/GNU/Emacs`（如果没有则手动添加项），在
  此项下添加字符串值，名称为HOME，值为你的Emacs目录（比如D:/Emacs24.3）。这一步使`.emacs.d`目录和`.emacs`文件
  位于Emacs目录下了（没有的话建立吧），方便换电脑是迁移Emacs。

##实用操作

* 获得前缀快捷键帮助：输入前缀快捷键，接`C-h`或`F1`键。
* 多行注释：选中多行，光标停留在最后一行行首，快捷键`C-x r t`，然后输入注释符。
* 多行反注释：选中多行，光标停留在最后一行注释符号右侧，快捷键`C-x r k`。

##常用快捷键

    C-x C-f 打开文件
    C-x C-s 保存文件
    C-x C-c 退出Emacs

    C-f 前进一个字符
    C-b 后退一个字符
    C-p 后退一行
    C-n 前进一行
    C-a 移到行首
    C-e 移到行尾
    C-v 向下翻页
    M-v 向上翻页
    M-< 缓冲区头部
    M-> 缓冲区尾部
    C-M-f 向前匹配括号
    C-M-b 向后匹配括号
    C-l 当前行居中
    
    M-n or C-u n 重复操作随后的命令n次
    C-u 重复操作随后的命令4次
    C-u C-u 重复操作随后的命令8次
    C-x ESC ESC 执行历史命令记录，M-p选择上一条命令，M-n选择下一条命令
    
    C-d 删除一个字符
    M-d 删除一个字
    C-k 删除一行
    M-k 删除一句
    C-w 删除标记区域
    C-y 粘贴删除的内容
    注意：C-y可以粘贴连续C-k删除的内容；先按C-y，然后按M-y可以选择粘贴被删除的内容
    
    C-@ 标记开始区域
    C-x h 标记所有文字
    C-x C-x 交换光标位置和区域标记区开头
    M-w 复制标记区域
    C-_ or C-x u 撤消操作
    
    C-x 0 关闭本窗口
    C-x 1 只留下一个窗口
    C-x 2 垂直均分窗口
    C-x 3 水平均分窗口
    C-x o 切换到别的窗口
    C-x s 保存所有窗口的缓冲
    C-x b 选择当前窗口的缓冲区
    C-x ^ 纵向扩大窗口
    C-x } 横向扩大窗口
    
    C-s key 向前搜索
    C-s 查找下一个
    ENTER 停止搜索
    C-r key 反向搜索
    C-s C-w 以光标所在位置的字为关键字搜索
    C-s C-s 重复上次搜索
    C-r C-r 重复上次反向搜索
    C-s ENTER C-w 进入单词搜索模式
    C-r ENTER C-w 进入反向单词搜索模式
    M-x replace-string ENTER search-string ENTER 替换
    M-% search-string ENTER replace-string ENTER 交互替换
    C-r 在进入查找/替换模式后，该命令进入迭代编辑模式
    C-M-x 退出迭代编辑模式，返回到查找/替换模式
    C-M-s 向前正则搜索
    C-M-r 向后正则搜索
    C-M-% 正则交互替换
    
    C-x C-b 打开缓冲区列表
    d or k 标记为删除
    ~ 标记为未修改状态
    % 标记为只读
    s 保存缓冲
    u 取消标记
    x 执行标记的操作
    f 在当前窗口打开该缓冲区
    o 在其他窗口打开该缓冲区

    C-x d 打开目录模式
    s 按日期/文件名排序显示
    v 阅读光标所在的文件
    q 退出阅读的文件
    d 标记为删除
    x 执行标记
    D 马上删除当前文件
    C 拷贝当前文件
    R 重命名当前文件
    + 新建文件夹
    Z 压缩文件
    ! 对光标所在的文件执行SHELL命令
    g 刷新显示
    i 在当前缓冲区的末尾插入子目录的内容
    [n]m 标记光标所在的文件，如果指定n，则从光标所在的文件起后n个文件被标记
    [n]u 取消当前光标标记的文件，n的含义同上
    t 反向标记文件
    %-m 正则标记
    q 退出目录模式
    说明：在目录模式中，如果输入!，在命令行中包含*或者?，有特殊的含义。*匹配当前光标所在的文件和所有标记的文件，?分别在每一个标记的文件上执行该命令。
    
##插件

插件安装步骤大致如下

* 把下载的插件放到某目录下（推荐放在`.emacs.d/plugins/`下，方便迁移）
* 在`.emacs`文件里添加配置代码

下面是两个常用插件的例子

把包括`yasnippet.el`在内的一包文件放到`~/.emacs.d/plugins/yasnippet`目录下，在`.emacs`文件内添加如
下代码。

{% highlight cl %}
(add-to-list 'load-path "~/.emacs.d/plugins/yasnippet")
(require 'yasnippet)
(yas-global-mode 1)
{% endhighlight %}

把包括`autocomplete.el`在内的一包文件放到`~/.emacs.d/plugins/auto-complete-1.3.1`目录下，在`.emacs`文件内添加如
下代码。

{% highlight cl %}
(add-to-list 'load-path "~/.emacs.d/plugins/auto-complete-1.3.1")
(require 'auto-complete) 
(require 'auto-complete-config) 
;(require 'auto-complete-settings) ; for test here.
(global-auto-complete-mode t) 
(add-to-list 'ac-dictionary-directories "~/.emacs.d/plugins/auto-complete-1.3.1/dict")
;(ac-config-default) ; for test here
(setq-default ac-sources '(ac-source-words-in-same-mode-buffers)) 
(add-hook 'emacs-lisp-mode-hook (lambda () (add-to-list 'ac-sources 'ac-source-symbols))) 
(add-hook 'auto-complete-mode-hook (lambda () (add-to-list 'ac-sources 'ac-source-filename))) 
(set-face-background 'ac-candidate-face "lightgray") 
(set-face-underline 'ac-candidate-face "darkgray") 
(set-face-background 'ac-selection-face "steelblue") 
(define-key ac-completing-map "\M-n" 'ac-next) 
(define-key ac-completing-map "\M-p" 'ac-previous) 
(setq ac-auto-start 1) 
(setq ac-dwim t) 
(define-key ac-mode-map (kbd "M-TAB") 'auto-complete) 
{% endhighlight %}

##杂项

* 自动备份的问题，设置`make-backup-files`变量
