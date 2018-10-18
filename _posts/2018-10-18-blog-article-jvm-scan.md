---
layout: post
title:  "jvm基础知识"
date:   2018-10-18 16:27:54
categories: jvm
tags: jvm
excerpt: java虚拟机基础知识
---


* content
{:toc}

#### JVM概念介绍
JVM是Java Virtual Machine（Java虚拟机）的缩写，它是通过仿真模拟各种实际计算机功能来实现的。
Java语言的特点“一次编译，到处运行”，关键是通过Java虚拟机来实现这一特点的。一般的高级语言至少需要编译成不同的目标代码才能在不同的平台上运行。Java语言使用Java虚拟机屏蔽了与具体平台相关的交互信息，使得Java语言编译程序只需生成在Java虚拟机上运行的目标代码（字节码），Java虚拟机将字节码解释成具体平台上的机器指令执行。

##### java平台逻辑结构图一览
![image](https://github.com/123456han/imagerepository/blob/master/image/jvm-module20181016.png?raw=true)

从图中可以看出jdk(java development kit)java开发工具箱与jre(java run environment)java运行环境的区别。
##### jvm结构图一览
<center>
<img src="https://github.com/123456han/imagerepository/blob/master/image/jvm-model-20181018.png?raw=true?raw=true" width="80%" height="80%" />
</center>
图中方法区和堆是线程共享的，java方法栈，本地方法栈，pc计数器为线程独享。

##### java代码编译
Java源码编译器完成java代码的编译，流程图如下所示：
![image](https://github.com/123456han/imagerepository/blob/master/image/java-sourcecode-compile-20181017.png?raw=true)

Java 源码编译流程图如下:
![image](https://github.com/123456han/imagerepository/blob/master/image/java-sourcecode-flow20181017.png?raw=true)
源码编译主要分为3个部分：
- 分析和输入到符号表
- 注解处理
- 语义分析和生成class文件
###### class文件的结构：

> 结构信息
 >> class文件格式版本号<br>
 >> 各部分的数量与大小

> 元数据
 >> 类、父类、实现接口的声明信息<br>
 >> 属性声明信息<br>
 >> 方法声明信息<br>
 >> 常量池

> 方法信息
 >> 字节码
 >> 异常处理器表
 >> 局部变量区的大小
 >> 操作数栈的大小
 >> 操作数栈的类型记录
 >> 调试用符号信息

##### 类加载
JVM的类加载是通过ClassLoader及其子类来完成的，类的层次关系和加载顺序如下图：
![image](https://github.com/123456han/imagerepository/blob/master/image/java-classload-mode20181017.png?raw=true)

- Bootstrap ClassLoader 启动类加载器

负责加载$JAVA_HOME中jre/lib/rt.jar里所有的class，由C++实现，不是ClassLoader子类

- Extension ClassLoader 扩展类加载器，父类为null

负责加载java平台中扩展功能的一些jar包，包括$JAVA_HOME中jre/lib/*.jar或-Djava.ext.dirs指定目录下的jar包，父类

- App ClassLoader  应用程序加载器

负责加载classpath中指定的jar包及目录中class，父类Extension ClassLoader

- Custom ClassLoader 自定义类加载器, 父类 App ClassLoader

属于应用程序根据自身需要自定义的ClassLoader，如tomcat、jboss都会根据j2ee规范自行实现ClassLoader加载过程中会先检查类是否被已加载，检查顺序是自底向上，从Custom ClassLoader到BootStrap ClassLoader逐层检查，只要某个classloader已加载就视为已加载此类，保证此类只所有ClassLoader加载一次。而加载的顺序是自顶向下逐层加载。

###### 双亲委派模型
JVM中类加载的机制——双亲委派模型。这个模型要求除了Bootstrap ClassLoader外，其余的类加载器都要有自己的父加载器。子加载器通过组合来复用父加载器的代码，而不是使用继承。在类加载器加载class文件时，它首先委托父加载器去加载这个类，依次传递到顶层类加载器(Bootstrap)。如果父加载器加载不了（它的搜索范围中找不到此类），子加载器才会加载这个类。

双亲委派模型的有效解决以下问题：

- 每一个类仅会被加载一次，避免了重复加载。
- 有效避免了某些恶意类的加载，Object类在程序的各种类加载器环境中都是同一个类。不会造成混乱。

双亲委派模型的实现在java.lang.ClassLoader的loadClass方法中
##### 类执行
JVM执行引擎完成java代码的执行，流程图如下所示：
![image](https://github.com/123456han/imagerepository/blob/master/image/jvm-execuate-qing-20181017.png?raw=true)

JVM是基于栈的体系结构来执行class字节码的。线程创建后，都会产生程序计数器（PC）和栈（Stack），程序计数器存放下一条要执行的指令在方法内的偏移量，栈中存放一个个栈帧，每个方法的每次调用会将栈帧压入方法栈，方法调用结束后会将此栈帧进行出栈。栈帧由局部变量区和操作数栈两部分组成，局部变量区用于存放方法中的局部变量和参数，操作数栈中用于存放方法执行过程中产生的中间结果。栈帧的结构如下图所示：
<center>
<img src="https://github.com/123456han/imagerepository/blob/master/image/java-stack-needle2018101714.png?raw=true" width="25%" height="25%" />
</center>

##### jvm内存模型
<center>
<img src="https://github.com/123456han/imagerepository/blob/master/image/java-inner-model-20181018.png?raw=true" width="80%" height="80%" />
</center>

- 程序计数器

程序计数器（Program Counter Register）是内存中一块较小的空间，它的作用当前线程所执行的字节码的行号指示器。根据这个计数器中存储的值来执行下一条字节码指令，分支、循环、跳转、异常处理线程恢复等功能都需要依赖这个计数器来完成。

- Java 虚拟机栈

Java 虚拟机栈（Java Virtual Machine Stacks）描述的是Java 方法执行的内存模型：每个方法被执行的时候都会同时创建一个栈帧（Stack Frame）用于存储局部变量表、操作数栈等信息。每一个方法被调用直至执行完成的过程，就对应着一个栈帧在虚拟机栈中从入栈到出栈的过程。


- 本地方法栈

本地方法栈（Native Method Stacks）是为虚拟机使用到的Native方法服务。执行过程与java虚拟机栈相似。

- 堆

Java 堆（Java Heap）是被所有线程共享的一块内存区域，在虚拟机启动时创建。此内存区域的唯一目的就是存放对象实例，所有的对象实例以及数组都要在堆上分配。

- 方法区

方法区（Method Area）线程共享的内存区域，它用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。

##### 内存溢出错误
内存溢出错误主要发生在：java堆，方法区，虚拟机栈，本地方法栈等。

###### java堆
- 异常：Exception in thread "main" java.lang.OutOfMemoryError: GC overhead limit exceeded

解释：GC overhead limt exceed检查是Hotspot VM 1.6定义的一个策略，通过统计GC时间来预测是否要OOM了，提前抛出异常，防止OOM发生。Sun 官方对此的定义是：“并行/并发回收器在GC回收时间过长时会抛出OutOfMemroyError。过长的定义是，超过98%的时间用来做GC并且回收了不到2%的堆内存。用来避免内存过小造成应用不能正常工作。“

- 异常：Exception in thread "main" java.lang.OutOfMemoryError: Java heap space

测试方法：
无限循环的new出对象来，在list中保存引用，以不被垃圾回收器回收。该区域也可能发生内存泄露。
-verbose:gc -XX:+PrintGCDetails  查看垃圾收集细节。
###### 方法区
测试方法：
生成大量的动态类，或无限循环调用String的intern()方法产生不同的对象实例，并在list中保存其引用，以不被垃圾回收器回收，后者测试常量池，前者测试方法区的非常量池部分。

###### 方法栈  
方法栈包括虚拟机栈和本地方法栈。

Exception in thread "main" java.lang.StackOverflowError

测试方法：

递归调用一个简单的方法会抛出StackOverflowError

。


