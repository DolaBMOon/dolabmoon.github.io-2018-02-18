---
layout: post
title: Josephus Problem
date: 2017-10-15 12:50:0 +0800
categories: technology
tags: 数学 DP 约瑟夫斯问题
img: 
---
准备了下初赛,然而发现有好多约瑟夫斯问题都不会...

# 约瑟夫斯问题

>准备了下初赛,然而发现有好多约瑟夫斯问题都不会...

首先是明确一下问题及其细节.

不,当然 是先讲故事辣.

>这个问题是以弗拉维奥·约瑟夫斯命名的，他是1世纪的一名犹太历史学家。他在自己的日记中写道，他和他的40个战友被罗马军队包围在洞中。他们讨论是自杀还是被俘，最终决定自杀，并以抽签的方式决定谁杀掉谁。约瑟夫斯和另外一个人是最后两个留下的人。约瑟夫斯说服了那个人，他们将向罗马军队投降，不再自杀。约瑟夫斯把他的存活归因于运气或天意，他不知道是哪一个。

问题是有n个人,从0开始标号(这样接下来的运算会比较方面,因为%%%),围成环状,数到第k个人就杀掉,再继续数数,问最后留下的是哪个人.

## k=2的特殊情况.

我们考虑一轮杀下来,再重新编号的话.

如果n%2==0,重新标号后位置为x的人就是
原来标号为![](http://latex.codecogs.com/gif.latex?x\times 2)的人

否则n%2==1,重新标号后位置为x的人就是原来表还为![](http://latex.codecogs.com/gif.latex?x\times 2+2)的人.

由此得出递推式

![](http://latex.codecogs.com/gif.latex?f(n)=2\times f(n/2)(n\%2==0))

![](http://latex.codecogs.com/gif.latex?f(n)=2\times f(\lfloor n/2\rfloor)+2(n\%2==1))

然后打出一张表

n=1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16

f(n)=0,0,2,0,2,4,6,0,2,4,6,8,10,12,14,0

可以发现

![](http://latex.codecogs.com/gif.latex?f(n)=2\times l(n=2^m+l,0<=l<2^m))

=将n的二进制最高位去掉再左移一位

**Proof:**

应用数学归纳法.嘛...oier不需要详细证明

## 一般情况

直接贴公式

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/f2b188d40bda947e356437f72241f02f0ff112b6)


