---
layout: post
title:  "队列"
date:   2018-11-06 18:11:54
categories: 数据结构与算法
tags: 数据结构 算法
excerpt: 队列
---

* content
{:toc}

### 队列
- 特点：先进者先出。
- 操作：入队enqueue()和出队dequeue()。。
- 实现：数组实现的队列叫作顺序队列（有界队列）；用链表实现的队列叫作链式队列（无界队列）。


#### 队列的分类
- 循环队列

将数组的首尾进行相连。解决数据搬移的问题。关键 确定队空和队满的条件。<br>
队空：head == tail 数组的头下标等于数组的尾下标。<br>
队满：(tail+1)%n=head  n为数组的长度。
- 阻塞队列

队列的基础上增加了阻塞操作。当队列为空的时候，从队头取数据就会阻塞，直到队列有了数据才能返回；当队列满的的时候，插入数据就会阻塞，直到队列中有空闲位置后再插入数据，然后再返回。

- 并发队列
线程安全的队列。简单的实现方式是直接在enqueue()、dequeue()方法加上锁，但锁粒度大并发度会比较低，同一时刻仅允许一个存或取操作。

#### 队列的应用
线程池，数据库连接池，分布式队列等。<br>
线程池没有空闲的线程时，新的任务请求线程资源时，一般有两种处理策略。
- 非阻塞的处理方式，直接拒绝任务任务请求。
- 阻塞的处理方式，将请求排队，等到有空闲的线程时，取出排队的请求继续处理。
实际上，对于大部分资源有限的场景，当没有空闲资源时，基本上都可以通过“队列”这种数据结构来实现请求队列。