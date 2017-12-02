---
layout: post
title: Euler Tour
date: 2017-12-02 22:01:0 +0800
categories: technology
tags: 数据结构
img: 
---

{%include latex.ext %}

# Euler Tour

## 首先

1. 它的功能是LCT的子集~~据我所知~~;
2. 比LCT还难写的功能就不讲了;

## 是什么

### 有一棵树:

           1
          / \
         2   5
        / \
       3   4
   

### 真的Euler Tour

1 2 3 3 2 4 4 2 1 5 5 1

### 假的Euler Tour

1 2 3 3 4 4 2 5 5 1

### DFS序...

1 2 3 4 5

### 边的Euler Tour

(1-2) (2-3) (3-2) (2-4) (4-2) (2-1) (1-5) (5-1)

可以用来维护一些边的信息吧

## 一些操作

默认用真的Euler Tour,只讲如何维护点的信息,维护边信息类似.

first(x)为x第一次出现的地方,last(x)为最后一次.

### LCA

lca(x,y)当然就是min(first(x),first(y))到max(last(x),last(y))最小dep的那个.

所以先O(nlogn)预处理就可以O(1)在线询问啦.

### 区间LCA

假设有一个序列a1,a2,a3...an

现在要求O(nlogn)预处理,O(1)在线询问:

ai...j的lca是哪个?

先做一遍LCA的预处理,现在我们可以O(1)得到Euler Tour上一段区间内的dep最小是哪个.

然后在a上倍增,维护一段$$ 2^k $$长度线段的first最小值和last最大值,这是可以O(1)合并的.

所以至此,预处理结束后就一切O(1)了.

### 动态维护到根的信息 

那就用假的Euler Tour.

假设是维护权值和:

1. 单点加:first(x)+=w,last(x)-=w;
2. 求x到根的和:返回序列上到first(x)的前缀和;

以上用树状数组啊什么的就可以维护了.

### link-cut

这要treap或者splay这种可以合并的数据结构.

一个子树一定是一段连续的区间,于是就link的时候直接merge进去,cut的时候直接split出来就好了.

### reroot

太假了,我可能尝试写过但...绝对没有LCT实惠,思考一下貌似还是两个log的.

以及我不会.

在江这东西的时候我可能会彻底忘掉.


