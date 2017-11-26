---
layout: post
title: 笛卡尔树
date: 2017-11-02 15:56:0 +0800
categories: technology
tags: 图论 数据结构 acm.sgu.ru
img: 
---
为什么呢,笛卡尔的英文读起来一点也不笛卡尔

# 笛卡尔树

## A Brief Introduction

[SGU 155](http://acm.sgu.ru/problem.php?contest=0&problem=155)

然而SGU经常炸,wo还是贴个题面~~以增加文章长度~~

>**155. Cartesian Tree**

>Let us consider a special type of binary search trees, called cartesian trees. Recall that a binary searchtree is a rooted ordered binary tree, such that for its every node x the following condition is satisfied: each node in its left subtree has the key less than the key of x, and each node in its right subtree has the key greater than the key of x. 
That is, if we denote the left subtree of the node x by L(x), its right subtree by R(x) and its key by kx, for each node x we will have 

>* if y in L(x) then ky < kx 
* if z in R(x) then kz > kx 

>The binary search tree is called cartesian if its every node x in addition to the main key kx also has an auxiliary key that we will denote by ax, and for these keys the heap condition is satisfied, that is 

>* if y is the parent of x then ay < ax 

>Thus a cartesian tree is a binary rooted ordered tree, such that each of its nodes has a pair of two keys (k, a) and three conditions described are satisfied. 
Given a set of pairs, construct a cartesian tree out of them, or detect that it is not possible.

>**Input**
The first line of the input file contains an integer number N - the number of pairs you should build cartesian tree out of (1 <= N <= 50000). The following N lines contain two integer numbers each - given pairs (ki, ai). For each pair |ki|, |ai| <= 30000. All main keys and all auxiliary keys are different, i.e. ki <> kj and ai <> aj for each i <> j.

>**Output**
On the first line of the output file print YES if it is possible to build a cartesian tree out of given pairs or NO if it is not. If the answer is positive, output the tree itself in the following N lines. Let the nodes be numbered from 1 to N corresponding to pairs they contain as these pairs are given in the input file. For each node output three numbers - its parent, its left child and its right child. If the node has no parent or no corresponding child, output 0 instead. 
If there are several possible trees, output any one.

>**Sample test(s)**

>Input
7 
5 4 
2 2 
3 9 
0 5 
1 3 
6 6 
4 11

>Output
YES 
2 3 6 
0 5 1 
1 0 7 
5 0 0 
2 4 0 
1 0 0 
3 0 0

### Solution

首先将其按照第一键值排序,以及然后最后插入的点一定在最右链的结尾.

so,用一个栈维护最右链.

插入一个点(设为o)的时候,在栈中找到一个断处,使得其上数(设为a)第二键值小于插入的,其下数(设为b)第二键值大于插入的,然后将插入的点作为a的右孩子,又由于o的第一键值是当前最大的,所以b作为o的左孩子.

```cpp
#include<iostream>
#include<algorithm>
#include<cstring>
#include<cstdio>
#include<cmath>
using namespace std;
const int MAXN=50000;
const int INF=0x3f3f3f3f;
struct Node{int id,k1,k2;};
int n,s[MAXN+10],top,fa[MAXN+10],lc[MAXN+10],rc[MAXN+10];
Node o[MAXN+10];
bool cmp(const Node& a,const Node& b){return a.k1<b.k1;}
int res[3][MAXN+10];
int main()
{
	scanf("%d",&n);
	for(int i=1;i<=n;++i)o[i].id=i,scanf("%d%d",&o[i].k1,&o[i].k2);
	sort(o+1,o+n+1,cmp);o[0].k1=o[0].k2=-INF;
	for(int i=1;i<=n;++i)
	{
		while(o[s[top]].k2>o[i].k2)--top;
		rc[s[top]]=i;fa[s[top+1]]=i;fa[i]=s[top];lc[i]=s[top+1];
		s[++top]=i;s[top+1]=0;
	}
	for(int i=1;i<=n;++i)
	{
		res[0][o[i].id]=o[fa[i]].id;
		res[1][o[i].id]=o[lc[i]].id;
		res[2][o[i].id]=o[rc[i]].id;
	}
	puts("YES");
	for(int i=1;i<=n;++i)printf("%d %d %d\n",res[0][i],res[1][i],res[2][i]);
	return 0;
}
```

## Application

1. 可以将区间最小转化为树上lca
2. O(k)每次寻找区间前k最值
3. wiki上看不懂的种种...
