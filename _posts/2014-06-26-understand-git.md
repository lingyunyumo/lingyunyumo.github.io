---
layout: post
title: "Git简明笔记"
tags: 
  - Git
---

## 前言

人人都说Git好，但不是人人熟练用着Git。

网上Git教程很多，但是看下来的感觉是：说的有理，看得也似乎明白，用起来则心慌慌。

接触Git很久了，最近忽然有顿悟感，记录成此文。

安装Git软件、初始化库、从Github等公共库克隆、如何提交commit等统统不再多说。

PS：[SourceTree](http://www.sourcetreeapp.com/)是个不错的Git图形化工具。下文没有必要的话不会出现具体的Git命令。

## 分支

首先，我们初始化了一个Git库，并提交了几次。

{% highlight Text %}
                     [HEAD]
                       ↓
                    [master]
                       ↓
【 0 】<--【 1 】<--【 2 】
{% endhighlight %}

Git里的分支可以类比成指针的概念。

[master]是默认的分支，它指向最近的一次提交【 2 】。

HEAD是Git的一个特殊的指针，它表明你当前在整个Git库的历史中的位置。

接下来，新建一个叫做[test]的分支。

{% highlight Text %}
                     [HEAD]
                       ↓
                    [master]
                       ↓
【 0 】<--【 1 】<--【 2 】
                       ↑
                    [test]
{% endhighlight %}

切换到[test]分支。

{% highlight Text %}
                    [master]
                       ↓
【 0 】<--【 1 】<--【 2 】
                       ↑
                     [test]
                       ↑
                     [HEAD]
{% endhighlight %}

可以看到HEAD已经从指向[master]改为指向[test]了。

此时我们再做些修改并提交commit。

{% highlight Text %}
                    [master]
                       ↓
【 0 】<--【 1 】<--【 2 】<--【 3 】
                                ↑
                              [test]
                                ↑
                              [HEAD]
{% endhighlight %}

由于我们之前切换到了[test]分支，所以所做的提交都是对于[test]分支而言的。

[test]分支已经领先[master]分支了，此时我们觉得[test]分支里的【 3 】改得不错，希望把它合并到[master]分支里。

合并操作是将某分支合并到当前分支，我们想把[test]分支合并到[master]分支，所以得先切换回[master]分支。

{% highlight Text %}
                     [HEAD]
                       ↓
                    [master]
                       ↓
【 0 】<--【 1 】<--【 2 】<--【 3 】
                                 ↑
                              [test]
{% endhighlight %}

将[test]分支合并到[master]分支。

{% highlight Text %}
                               [HEAD]
                                 ↓
                              [master]
                                 ↓
【 0 】<--【 1 】<--【 2 】<--【 3 】
                                 ↑
                              [test]
{% endhighlight %}

这次合并确切地说应该是“快速合并”，实际只是将master指针从【 2 】移动到了【 3 】。

接下来，我们在[test]分支和[master]分支上各做一次提交commit，并保持[master]分支为当前分支。

{% highlight Text %}
                                    [HEAD]
                                      ↓
                                   [master]
                                      ↓ 
                                    【 4 】
                                  ↙
【 0 】<--【 1 】<--【 2 】<--【 3 】 
                                  ↖
                                   【 5 】
                                      ↑
                                    [test]
{% endhighlight %}

将[test]分支合并到[master]分支。如果运气不错，没有冲突，合并便顺利成功。

{% highlight Text %}
                                               [HEAD]
                                                 ↓
                                              [master]
                                                 ↓ 
                                    【 4 】<--【 6 】
                                  ↙         ╱
【 0 】<--【 1 】<--【 2 】<--【 3 】      ╱
                                  ↖     ↙
                                   【 5 】
                                     ↑
                                   [test]
{% endhighlight %}

这次合并有别于上面的“快速合并”，Git计算了两条分支的差异，并生成了一个新的提交【 6 】。注意观察master、test、HEAD指针的位置。

如果运气不佳，两条分支上修改了同一个文件同位置的内容，Git就不知道怎么处理了，此为“冲突”。冲突需要你手动修改，然后重新合并。

## 远端

你克隆了一个远端的Git库。

{% highlight Text %}
         [origin/HEAD]     [HEAD]
               ↓            ↓
        [origin/master]   [master]
                     ↘  ↙
【 0 】<--【 1 】<--【 2 】
{% endhighlight %}

这个“origin”代表远端库。[origin/master]是远端的分支，与本地的[master]分支是不同的分支。

当前分支为本地的master分支，做一些改动。

{% highlight Text %}
                [origin/HEAD]   [HEAD]
                       ↓        ↓
              [origin/master]   [master]
                       ↓        ↓ 
【 0 】<--【 1 】<--【 2 】<--【 3 】
{% endhighlight %}

此时本地的[master]分支领先于远端的[origin/master]，通过推送push将本地的改动合并到远端。

{% highlight Text %}
                  [origin/HEAD]       [HEAD]
                        ↓              ↓
                 [origin/master]    [master]
                              ↘    ↙
【 0 】<--【 1 】<--【 2 】<--【 3 】
{% endhighlight %}

接下来，假设有其他人讲改动推送push到了同一个远端。我们抓取fetch一下，可能会是下面的情况（视他人所做的改动）。

{% highlight Text %}
                               [HEAD]   [origin/HEAD]
                                 ↓        ↓
                             [master]   [origin/master]
                                 ↓        ↓
【 0 】<--【 1 】<--【 2 】<--【 3 】<--【 4 】
{% endhighlight %}

可以看到，由于别人的改动，[origin/master]分支反而领先于[master]分支了。

我们可以切换到[master]分支，然后将[origin/master]分支合并merge到[origin/master]分支，将本地紧跟远端公共库，不至于变得out（别忘了Git是协作编程神器）。

{% highlight Text %}
                                   [HEAD]   [origin/HEAD]
                                     ↓        ↓
                                 [master]   [origin/master]
                                        ↘   ↙
【 0 】<--【 1 】<--【 2 】<--【 3 】<--【 4 】
{% endhighlight %}

其实，另外有个拉取pull命令，等价于上面的抓取fetch和合并merge的效果总和。

## 心得

用git的分支是有个问题，两条分支分叉的太远，合并时产生冲突的概率也会增高。

假设有两个分支master和test，master是稳定的主分支，test是我为了测试一项实验性的新特性
而建的分支。我在test上做了不少提交，同时同伴们在master上也做了不少提交，但是test有尚未
到可以合并merge到master分支的时候。

这种情况下，可以频繁的将master分支合并到test分支，有冲突也是少量的不难解决的。此操作对master
分支没有任何改动。