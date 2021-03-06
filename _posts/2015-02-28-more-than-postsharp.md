---
layout: post
title: "PostSharp引起的思考：程序设计方法"
tags: 
  - PostSharp
  - 面向对象
  - 面向切面
---


最近，在寻找能优雅的实现日志功能的方法，避免重复地书写雷同的代码。不久，搜索到面向切面编程（AOP）的概念。面向切面编程（AOP）是不同于面向对象编程（OOP)的一种思想，使用的场景有日志记录、权限验证等，具体可搜索引擎之。

很自然的，找到了.Net下的AOP框架PostSharp，稍加试验就被PostSharp和AOP深深地吸引了。

发觉这次不仅仅是技术上的积累，意外的激发了对程序设计方法的思考。

截止此刻，自己编程思想的进化大致经历了：

1. 初学编程时不自知地在使用面向过程编程的思想，谈不上方法论的阶段
2. 在面向对象编程的思想范畴里从生疏到熟练，但方法论长期未变
3. 发现了面向切面编程的思想

面向对象编程的思想，让我体会到了程序与现实的内在相同，大大的提高了我对编程的热爱。

感谢第3点的出现，让我认识到自己长期处于第2点面相对对象思想的限制中。

就算眼前的事物再美好，也不要停止思考更多的可能性。

写着写着就忘了开始写此篇时的point是什么，思路渐渐走样了。就此打住，仅此记录一次中断的思考。


技术备忘：

解决某个Project不启用PostSharp的问题：Project属性，添加了PostSharp一页，里面某项“此项目禁止PostSharp”默认设置时Yes！




