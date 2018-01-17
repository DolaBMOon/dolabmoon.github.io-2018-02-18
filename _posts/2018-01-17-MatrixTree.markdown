---
layout: post
title: 矩阵树定理
date: 2018-01-17 19:48:0 +0800
categories: technology
tags: 数学
img: 
---

{% include latex.ext %}

[推荐阅读](http://vfleaking.blog.163.com/blog/static/1748076342013112523651955/)

# 矩阵树定理

## 无向图

一个无向图的生成树个数为det(其[拉普拉斯矩阵](https://en.wikipedia.org/wiki/Laplacian_matrix)去掉一行一列)

## 有向图

和无向图类似地,首先拉普拉斯矩阵去掉的一行一列为根节点,其次如果:

1. 想要的树形图是从叶子指向根的,那么拉普拉斯矩阵中的度数改为入度;

2. 想要的树形图是从根指向叶子的,那么拉普拉斯矩阵中的度数改为出度.
