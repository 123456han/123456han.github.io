---
layout: post
title:  "红黑树"
date:   2018-09-28 17:30:54
categories: 数据结构与算法
tags: 红黑树
excerpt: 红黑树的概念和性质
---

* content
{:toc}

## 红黑树
红黑树是许多“平衡”搜索树中的一种，保证最坏的情况下基本动态集合操作的时间复杂度为O(lgn);

### 性质
- 每个结点或是红色的，或是黑色的。
- 根结点是黑色的
- 每个叶结点(NIL)是黑色的
- 对每个结点，从该结点到其所有后代叶结点的简单路径上，均含有相同数目的黑色结点。

### 红黑树插入结点的情况
- 插入z的叔结点y是红色的。
- 插入z的结点叔结点y是黑色的且z是一个右孩子
- 插入z的结点叔结点y是黑色的且z是一个左孩子

### 红黑树删除结点的情况
- x的兄弟结点w是红色的
- x的兄弟结点w是黑色的，而且w的两个子结点都是黑色的。
- x的兄弟结点w是黑色的，w的左孩子是红色的，w的右孩子是黑色的。
- x的兄弟结点w是黑色的，且w的右孩子是红色的。      

## 后续