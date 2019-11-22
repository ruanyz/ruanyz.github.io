---
id: 116
title: 校验和的计算
date: 2019-07-09T16:42:51+08:00
author: MR. ruan
layout: revision
guid: http://www.ruanyz.world/116.html
permalink: /116.html
---
之前一直只是对tcp，udp，ip校验和的计算方法有点了解，但是没有真正的手工计算过。今天找了一个包根据其给的checksum的值与自己手动计算的值进行对比。

一般校验和的计算方法：

将需要计算校验和的数据按两字节一组划分，进行累加，若为奇数，源数据尾部添加0x00。将超出16bit数据取出远16bit数据相加后取反即为checksum

  1. 首先来看看简单的IP checksum。将20字节的ip头按两字节一组连续相加，遇到checksum，跳过。最后将超出数据取出与当前数据相加后取反。<figure class="wp-block-image">

<img src="http://www.ruanyz.world/wp-content/uploads/2019/07/image-1.png" alt="" class="wp-image-115" srcset="http://www.ruanyz.world/wp-content/uploads/2019/07/image-1.png 603w, http://www.ruanyz.world/wp-content/uploads/2019/07/image-1-300x40.png 300w" sizes="(max-width: 603px) 100vw, 603px" /> </figure> 

  1. 再来看看比较难的udp checksum，需要按照以下3个部分计算。首先是payload数据，然后是udp头部：包含两个port，udp长度（udp头+payload长度）。最后是亚头部，包含两个ip地址，  
    当前协议类型 和udp长度（udp头+payload长度）。下图给出具体事例：首先payload的数据累加为：2642d，udp头部为2端口+1长度=7600，亚头部为两ip addr+协议类型+udp长度=xxx+0x11+0x1d=107ab<figure class="wp-block-image">

<img src="http://www.ruanyz.world/wp-content/uploads/2019/07/image.png" alt="" class="wp-image-114" srcset="http://www.ruanyz.world/wp-content/uploads/2019/07/image.png 637w, http://www.ruanyz.world/wp-content/uploads/2019/07/image-300x43.png 300w" sizes="(max-width: 637px) 100vw, 637px" /> <figcaption>  
</figcaption></figure>