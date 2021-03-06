---
layout: post
title:  "栈"
date:   2018-11-06 13:11:54
categories: 数据结构与算法
tags: 数据结构 算法
excerpt: 栈
---

* content
{:toc}

### 栈
- 特点：后进者先出，先进者后出。只允许在一端插入和删除数据。
- 操作：入栈和出栈。
- 实现：数组实现称为顺序栈；链表实现称为链式栈。
- 复杂度：空间复杂度和时间复杂度都是O(1)

特定的数据结构是对特定场景的抽象。
#### 栈的应用
- 栈在函数调用中的应用

jvm内存结构：函数调用在方法栈中，通过栈帧的入栈和出栈来完成函数的调用。

- 栈在表达式中求值的应用

编译器通过两个栈来实现的。一个栈用于保存操作数；一个栈用于保存运算符。从左向右遍历表达式，当遇到数字，我们就直接压入操作数栈，当遇到运算符，就与运算符栈的栈顶元素的优先级进行比较。如果比运算符站符栈顶元素的优先级高，就将当前的运算符压入栈；如果比运算符栈顶元素的优先级低或者相同，从运算符栈中取栈顶运算符，从操作数栈的栈顶取2个操作数，然后进行计算，再把计算完的结果压入操作数栈，继续比较。

- 栈在括号匹配中的应用

用栈保存未匹配的左括号，从左到右依次扫描字符串。当扫描到左括号时，则将其压入栈；当扫描到右括号时，从栈顶取出一个左括号。如果能够匹配，比如"("与")"匹配，"["与"]"匹配，"{"与"}"匹配，则继续扫描剩下的字符串。如果扫描过程中，遇到不能匹配的右括号，或者栈中没有数据，则说明是非法格式。当所有的括号都扫描完成后，如果栈为空，则说明字符串是合法格式；否则，说明未匹配的左括号，为非法格式。
