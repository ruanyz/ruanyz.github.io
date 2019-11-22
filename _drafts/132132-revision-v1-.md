---
id: 133
date: 2019-09-21T17:42:32+08:00
author: MR. ruan
layout: revision
guid: http://www.ruanyz.world/133.html
permalink: /133.html
---
在Linux下对层次比较深的文件夹操作时，需要记录很长的文件路径，同时每次输入也相当麻烦。可以将需要操作常用命令添加到~/.bashrc文件中，使用这种格式：alias my\_custom\_pwd = cd &#8220;cd $(pwd)/home/yuanong&#8221;。

Linux下经常对文件进行压缩和解压：

tar cf tt.tar ./file.txt 压缩文件

tag xf ./tt.tar 解压文件

tag tf ./tt.tar 查看压缩文件内容

cat /proc/cupinfo 

cat /proc/meminfo

vim 操作