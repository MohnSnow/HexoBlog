---
title: Paxos算法
date: 2017-03-07 16:20:27
tags: Paxos
categories: "技术"
toc: true
---
### 概述
Paxos算法是Lamport创造基于消息传递的一致性算法，包括Google的Chubby在内很多系统都应用了Paxos算法，Google Chubby[1]有下面的描述：
```
all working protocols for asynchronous consensus we have so far encountered have Paxos at their core.
```
足见该算法在分布式系统中的地位。
<!--more-->
### 背景说明
Paxos解决的问题是，在分布式系统中系统间如何就一个不可变变量达成一致，仅此而已！但是在该算法的基础之上我们可以做非常有意义的事情，比如Google Chubby就是对Multi-Paxos算法的工程实现，Multi-Paxos
算法的基础就是Paxos，通俗来说，就是多个轮次的Paxos算法的执行，确定一系列不可能变量的值，如果各个节点初始状态一致，再执行相同的操作序列（即确定的一系列不可变变量的值），那么最终结果必然也是一致的。这是可以应用于系统容错和系统一致性上的。