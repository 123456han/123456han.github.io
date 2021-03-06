---
layout: post
title:  "链表"
date:   2018-11-02 11:20:54
categories: 数据结构与算法
tags: 数据结构 算法
excerpt: 链表
---

* content
{:toc}

### 链表
常用的链表
- 单向链表
- 双向链表 LinkedHashMap
- 循环链表 解决约瑟夫问题
#### LRU缓存淘汰算法  
缓存思想 空间换时间
- 先进先出策略FIFO（first in, first out）
- 最少使用策略LFU（Least Frequently Used）
- 最近最少使用策略LRU（Least Recently used）
#### 数组与链表的区别

区别 |数组 | 链表
---|---|---
内存 | 连续的内存 | “指针”串联起零散得内存块
随机访问 | O(1) | O(n)
插入删除 | O(n) | O(1)

#### 思想
对于执行较慢的程序，可以通过消耗更多的内存（空间换时间）来进优化；
消耗过多内存的程序，可以通过消耗更多时间（时间换空间）来降低内存消耗。
- 空间换时间  缓存 空间复杂度较高，时间复杂度较低的算法或数据结构。
- 时间换空间  
#### 链表操作
常用  快慢两个指针的遍历
- 单链表反转
- 链表中环的检测
- 两个有序链表合并
- 删除链表倒数第n个结点
- 求链表的中间结点
#### 链表代码技巧
- 理解指针和引用的含义

将某个变量赋值给指针，实际上就是将这个变量的地址赋值给指针，或者反过来说，指针中存储了这个变量的内存地址，指向了这个变量，通过指针就能找到这个变量。

- 警惕指针丢失和内存泄露
- 利用哨兵简化实现难度
- 重点留意边界条件的处理。
- 举例画图，辅助思考。
- 多写多练，没有捷径

边界条件：链表为空；链表只包含一个结点，链表只包含两个结点，处理头尾结点。
#### 注意
针对链表的插入、删除操作，需要对插入第一个结点和删除最后一个结点的情况进行特殊处理。



