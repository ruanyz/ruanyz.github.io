---
id: 75
title: FPGA代码编写的心得（一）
date: 2018-12-16T23:06:33+08:00
author: MR. ruan
layout: revision
guid: http://www.ruanyz.world/75.html
permalink: /75.html
---
最近在公司修改MD的组包逻辑，自己在编写代码时。首先需要弄清几个信号间的时序关系，这点很重要，如果时序逻辑的数据发生延时，那么其对于的其他信号，如：读写使能，空、满标志也需要相应的延时，这里涉及到延时时，又有一点需要注意，有的信号指示单纯的延时一个时钟周期，而有的信号的延时需要添加相关条件。例如：从fifo中读出一个数据，对读出的数据进行计数，那么其不是每个时钟都有数据输出有效的，那么这样的延时，我们可能需要将某个时钟计数器的值间存在+1、-1的关系。下面使用代码举例：

always@（POSedge  clk or posedge rst）

if(rst)begin  cout<=0;

count_d1<=0; end

else begin  count _d1<=count;

count<=count+1;

end

&nbsp;

always@（POSedge  clk or posedge rst）

if(rst)begin  cout<=0;

count_d1<=0; end

else if (!fifo\_empty && read\_fifo) begin     //数据延时需要条件

count<=count+1;

count_d1<=count;

end

&nbsp;

接下来讲讲组合逻辑和时序逻辑：组合逻辑也就是数据的状态与时钟没有关系，单数据变化时，立即响应，没有延时一个时钟。最常见的就是case语句的多判断形式的组合逻辑。而对于时序逻辑，也就是在在时钟的上下边沿触发，接着判断条件，进行数据操作，会延时一个时钟输出。

&nbsp;

&nbsp;

&nbsp;