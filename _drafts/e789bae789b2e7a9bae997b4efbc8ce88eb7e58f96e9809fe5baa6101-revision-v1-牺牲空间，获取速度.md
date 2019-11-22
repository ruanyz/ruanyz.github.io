---
id: 107
title: 牺牲空间，获取速度
date: 2019-01-18T14:37:15+08:00
author: MR. ruan
layout: revision
guid: http://www.ruanyz.world/107.html
permalink: /107.html
---
 

在进行调试crc冲突的时候，想通过时间延时来解决地址冲突的问题“

原来的思想：直接将那么进行crc编码，然后选择编码的低10 bit作为ram块地址进行存储和更新，之前使用固定的状态机，也就是在只进行获取crc数据-》读数据-》判读-》更新。但是存在不同的name具有相同的crc数据

我的思想是：延时一包数据，也就是第一包数据正常求取地址并且进行name一致性判断，如果存在占用，那么地址++。这样在下一包时，可以获取真确的ram地址。在正常情况下，可以是实现。但是在异常下，如错包时，怎么判断呢？如下所示：<figure class="wp-block-image">

<img src="http://www.ruanyz.world/wp-content/uploads/2019/01/1.png" alt="" class="wp-image-103" srcset="http://www.ruanyz.world/wp-content/uploads/2019/01/1.png 621w, http://www.ruanyz.world/wp-content/uploads/2019/01/1-300x55.png 300w" sizes="(max-width: 621px) 100vw, 621px" /> </figure> <figure class="wp-block-image"><img src="http://www.ruanyz.world/wp-content/uploads/2019/01/2-1024x464.png" alt="" class="wp-image-104" srcset="http://www.ruanyz.world/wp-content/uploads/2019/01/2-1024x464.png 1024w, http://www.ruanyz.world/wp-content/uploads/2019/01/2-300x136.png 300w, http://www.ruanyz.world/wp-content/uploads/2019/01/2-768x348.png 768w, http://www.ruanyz.world/wp-content/uploads/2019/01/2.png 1455w" sizes="(max-width: 767px) 89vw, (max-width: 1000px) 54vw, (max-width: 1071px) 543px, 580px" /></figure> 

这种情况下的时序很难调整，而多次的ram读写导致输出的时间也是不可控制的，所以代码实现较难。为了和原来的逻辑一样，这里选择使用多个ram进行缓存，也就是将原始的ram进行copy，当有冲突时，选备选ram。自己的逻辑是先读再写的，这就可以在一个时钟间将两个ram的数据同时读出进行判断。与原来的状态机时序一致，只是增加两个ram的判断逻辑。

之前想法<figure class="wp-block-image">

<img src="http://www.ruanyz.world/wp-content/uploads/2019/01/3.png" alt="" class="wp-image-105" srcset="http://www.ruanyz.world/wp-content/uploads/2019/01/3.png 648w, http://www.ruanyz.world/wp-content/uploads/2019/01/3-300x182.png 300w" sizes="(max-width: 648px) 100vw, 648px" /> </figure> 

现在想法，已经实现，但是很费空间。<figure class="wp-block-image">

<img src="http://www.ruanyz.world/wp-content/uploads/2019/01/4.png" alt="" class="wp-image-106" srcset="http://www.ruanyz.world/wp-content/uploads/2019/01/4.png 510w, http://www.ruanyz.world/wp-content/uploads/2019/01/4-300x242.png 300w" sizes="(max-width: 510px) 100vw, 510px" /> </figure>