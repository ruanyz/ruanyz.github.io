---
id: 98
title: 怎么进行时序对齐
date: 2019-01-13T21:29:14+08:00
author: MR. ruan
layout: revision
guid: http://www.ruanyz.world/98.html
permalink: /98.html
---
上两周一直在写一些小的模块，虽然是简单的练习，但是单独的去写，只要了解功能，就进行逻辑实现就行了。但是如果在原来代码的基础上进行升级修改，例如：在前后级之间插入一个新的模块，那么你编写的模块必须保证后继模块与前级模块的时序对其，也就是如果没有你加入的模块，原来的输出信号数据与输入信号间必然存在时序关系，如果你添加的模块存在reg，也就是存在延时，那么你相应的输出需要延时。

这个也让我想起来，以前看代码都是喜欢图形化的界面，也及时net view。但是师兄他们都是之间看代码，搜索输入输出信号名字，然后理解逻辑关系，而我的那种看代码的方式，也只能是看了输入输出接口怎么连接的，也有可能只是引出来，在下级模块并没有使用。所以真正的看代码还是需要着重于了解模块的功能；模块的输入输出接口间的实现关系，在现在的company，主要是状态机的逻辑关系，也就是状态变迁的条件，这个十分关键。

另外讲讲最近编码的一些反思：可以自定义reg信号，标记某些未知状态，便于查错；自己编写了逻辑，但是不输出，那么就需要一级一级的查找你的信号在什么添加下输出，也就是你的条件十分触发（满足）。不然就是代码问题，自己遇到的就是判断相等，由于位宽错位，导致判断逻辑错误。