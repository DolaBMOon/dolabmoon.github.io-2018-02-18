---
layout: post
title: 二次剩余
date: 2017-11-01 10:56:0 +0800
categories: technology
tags: 数学
img: 
---
当然我只会质数的情况

# 二次剩余

一下均在质数二次剩余内部讨论

## 非实在二次剩余及其内部の辩证关系

设a,b是任意二次剩余,c,d是任意二次非剩余.

1. 易得a的逆元也是二次剩余
2. b的逆元也不是二次剩余,如果b的逆元是二次剩余,那么由1得b的逆元的逆元也就是b也是二次逆元,矛盾
3. ![](http://latex.codecogs.com/gif.latex?a\times b)是二次剩余,当然啦
4. ![](http://latex.codecogs.com/gif.latex?a\times c)不是二次剩余,可以脑补一下,对于![](http://latex.codecogs.com/gif.latex?a\times (x=1...p-1)),各个数不相同,然后当x是二次剩余的时候,其结果必然是二次剩余(因为3),然后留给非二次剩余的也必然是二次非剩余
5. ![](http://latex.codecogs.com/gif.latex?c\times d)是二次剩余,利用同样的上述方法,脑补一下咯

## 质数二次剩余の判别

p=2时所有自然数都是其二次剩余,以及以下p均为奇素数.

x是p的二次剩余,当且仅当

![](http://latex.codecogs.com/gif.latex?x^{p-1\over 2}\equiv1(mod\ p))

首先由于p是个质数

![](http://latex.codecogs.com/gif.latex?x^{p-1}\equiv 1)

然后p-1是个偶数

![](http://latex.codecogs.com/gif.latex?(x^{p-1\over 2}-1)\times (x^{p-1\over 2}+1)\equiv 0)

所以

![](http://latex.codecogs.com/gif.latex?x^{p-1\over 2}\equiv -1\ or\ 1)

然而以上大概并没有什么用

如果x是个二次剩余那![](http://latex.codecogs.com/gif.latex?x^{p-1})是二次剩余,因此可以开方成![](http://latex.codecogs.com/gif.latex?x^{p-1\over 2}),然后1本来也就可以开方成1,然后就证明了它的必要性,当然我是不会证充分性的
