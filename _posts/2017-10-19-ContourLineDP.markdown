---
layout: post
title: 轮廓线DP
date: 2017-10-19 19:02:0 +0800
categories: technology
tags: DP 轮廓线DP
img: 
---
dynamic programming

# 轮廓线DP

## Hardwood floor

[sgu 131](http://acm.sgu.ru/problem.php?contest=0&problem=131)
>time limit per test: 0.25 sec. 
memory limit per test: 4096 KB

The banquet hall of Computer Scientists' Palace has a rectangular form of the size M x N (1<=M<=9, 1<=N<=9). 

It is necessary to lay hardwood floors in the hall. There are wood pieces of two forms:

1. rectangles (2x1) 
2. corners (squares 2x2 without one 1x1 square) 

You have to determine X - the number of ways to cover the banquet hall. 

Remarks. The number of pieces is large enough. It is not allowed to leave empty places, or to cover any part of a surface twice, or to saw pieces.

**Input**

The first line contains natural number M. The second line contains a natural number N.

**Output**

First line should contain the number X, or 0 if there are no solutions.

**Sample Input**

> 2 3
 
**Sample Output**

 >5

### Solution:

占坑

### Code:

```cpp
#include<iostream>
#include<algorithm>
#include<cstring>
#include<cstdio>
#include<cmath>
using namespace std;
#define ll long long
const int MAXN=15;
int n,m,S,cur;
ll f[2][(1<<MAXN)+10];
void Dark(int a,ll w){if(a&1)f[cur][a>>1]+=w;}
int main()
{
	scanf("%d%d",&n,&m);if(n<m)swap(n,m);
	S=(1<<(m+1))-1;f[cur][S]=1;
	for(int i=0;i<n;++i)
	{
		for(int j=0;j<m;++j)
		{
			cur^=1;memset(f[cur],0,sizeof(f[cur]));
			for(int k=0;k<=S;++k)
			{
				Dark(k,f[cur^1][k]);
				if(i&&!(k&2))Dark(k^2^(1<<(m+1)),f[cur^1][k]);
				if(j&&!(k&(1<<m)))Dark(k^(1<<m)^(1<<(m+1)),f[cur^1][k]);
				if(i&&j&&!(k&2)&&!(k&(1<<m)))Dark(k^2^(1<<m)^(1<<(m+1)),f[cur^1][k]);
				if(i&&j&&!(k&1)&&!(k&2))Dark(k^1^2^(1<<(m+1)),f[cur^1][k]);
				if(i&&j&&!(k&1)&&!(k&(1<<m)))Dark(k^1^(1<<m)^(1<<(m+1)),f[cur^1][k]);
				if(i&&j&&!(k&1)&&!(k&2)&&!(k&(1<<m)))Dark(k^1^2^(1<<m),f[cur^1][k]);
			}
		}
	}
	printf("%lld",f[cur][S]);
	return 0;
}
```
