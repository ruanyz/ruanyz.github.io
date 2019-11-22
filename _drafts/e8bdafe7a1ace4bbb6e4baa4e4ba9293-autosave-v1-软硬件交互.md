---
id: 96
title: 软硬件交互
date: 2018-12-29T08:43:28+08:00
author: MR. ruan
layout: revision
guid: http://www.ruanyz.world/96.html
permalink: /96.html
---
The PCI Express Root Port is a port on the root complex  


在Linux系系统中实现虚拟内存的映射关系，在软件这边主要是使用了mmap函数！

**v****oid** **\*mmap(void \*start, size\_t length, int prot, int flags, int fd, off\_t offset);****函数实例**

函数参数说明：

  * **Start：**指向欲映射的内存起始地址，通常设为 NULL，代表让系统自动选定地址，映射成功后返回该地址。
  * **Length：**文件中有多大部分映射到内存
  * **Prot：**映射区域的保护方式，包含以下一种或多种组合：
      * PROT_EXEC 映射区域可被执行
      * PROT_READ 映射区域可被读取
      * PROT_WRITE 映射区域可被写入
      * PROT_NONE 映射区域不能存取
  * **Flags：**影响映射区域的各种特性，在调用mmap()时必须要指定MAP\_SHARED 或MAP\_PRIVATE。
      * MAP_FIXED 如果参数start所指的地址无法成功建立映射时，则放弃映射，不对地址做修正。通常不鼓励用此标志。
      * MAP_SHARED对映射区域的写入数据会复制回文件内，而且允许其他映射该文件的进程共享。
      * MAP_PRIVATE 对映射区域的写入操作会产生一个映射文件的复制，即私人的“写入时复制”（copy on write）对此区域作的任何修改都不会写回原来的文件内容。
      * MAP_ANONYMOUS建立匿名映射。此时会忽略参数fd，不涉及文件，而且映射区域无法和其他进程共享。
      * MAP_DENYWRITE只允许对映射区域的写入操作，其他对文件直接写入的操作将会被拒绝。
      * MAP_LOCKED 将映射区域锁定住，这表示该区域不会被置换（swap）。
  * Fd：要映射到内存中的文件描述符。有些系统不支持匿名内存映射，则可以使用fopen打开/dev/xx文件，然后对该文件进行映射，可以同样达到匿名内存映射的效果。
  * Offset: 文件映射的偏移量，通常设置为0，代表从文件最前方开始对应，offset必须是分页大小的整数倍。
  * 返回值：若映射成功则返回映射区的内存起始地址，否则返MAP_FAILED(－1)，错误原因存于errno 中。



在实例中，使用将硬件定义的区间（包含寄存器配置，dma读写位置等）与软件这边的mmap的虚拟地址映射起来，那么当硬件那边存在数据变化时，软件这边就开始将虚拟映射的位置存入一个新的内存空间。需要注意软硬件映射的区块大小，这样有助于软硬件数据的交互，不要