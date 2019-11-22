---
id: 126
title: Perl常用操作
date: 2019-09-20T08:43:29+08:00
author: MR. ruan
layout: revision
guid: http://www.ruanyz.world/126.html
permalink: /126.html
---
Date ： 2019.09.17，18

  * Perl
      * 变量和数组
          * 变量申明 &nbsp;&nbsp;&nbsp;&nbsp;my $var=0; &nbsp;&nbsp;&nbsp;&nbsp; my $var=””;
          * 数组申明 &nbsp;&nbsp;&nbsp;&nbsp;my @var
      * 逻辑运算
          * 字符&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Eq&nbsp; ne
          * 数据&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; > &nbsp;&nbsp;&nbsp;&nbsp; <&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; >=&nbsp;&nbsp; <=&nbsp; ==
      * 主要是有关文件读写,关键字数据的提取及逻辑检测，删除文件几行(使用tie::file)
      * 对于文件的读取直接将文件名字与file hander捆绑起来，使用hander就可以对文件的一行数据进行读取和处理了。获取到一行数据，可以使用split+分隔符形式将一行数据切割成一个数组元素(@var)，然后使用$var[0],$var[1]对元素进行访问；对于具有固定格式的行数据，可以根据substr使用确切的位置对字符串拆分。

  * SUBSTR
      * substr EXPR,OFFSET,LENGTH,REPLACEMENT
      * substr EXPR,OFFSET,LENGTH
      * substr EXPR,OFFSET
  * SPLIT
      * split(/\d+/, $data); &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 只输出切割后的非数字数据
      * split(/(\d+)/, $data);&nbsp;&nbsp;&nbsp; 同时保证输出用于切割的数字
      * 使用hash切割

#!/usr/bin/perl

&nbsp; use strict;

&nbsp; use warnings;

&nbsp; my $data = &#8216;FIRSTFIELD=1;SECONDFIELD=2;THIRDFIELD=3&#8217;;

&nbsp; my %values =&nbsp; split(/[=;]/, $data);

&nbsp; foreach my $k (keys %values) {

&nbsp;&nbsp;&nbsp; print &#8220;$k: $values{$k}\n&#8221;;

&nbsp; }

&nbsp; exit 0;

result&nbsp; is ：

&nbsp; FIRSTFIELD: 1

&nbsp; THIRDFIELD: 3

&nbsp; SECONDFIELD: 2

  * regular expressions:
      * /(d+)/&nbsp;&nbsp; /m(pattern)/
  * 格式化输出
      * Print FILE_HANDER “data”； &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 只可以将数据写入文件
      * Printf FILE_HANDER “%-20s,%d,%d”,$var1,var2,$var3&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 将数据格式化写入文件
      * 语法

format FormatName =

fieldline

value\_one, value\_two, value_three

fieldline

value\_one, value\_two

&nbsp;&nbsp; .