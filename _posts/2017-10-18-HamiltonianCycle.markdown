---
layout: post
title: 哈密顿回路
date: 2017-10-18 15:54:0 +0800
categories: technology
tags: 图论 哈密顿回路 codeforces.com acm.sgu.ru
img: 
---
Hamiltonian Cycle

# 哈密顿回路

## 满足ore性质的哈密顿回路

[sgu122](http://acm.sgu.ru/problem.php?contest=0&problem=122)

>ore性质是说任意两点的度数之和>=n

哈密顿回路要怎么求呢.

1. 首先将一个点作为一条哈密顿链

2. 将链的首尾尽可能扩展.

3. 在上面找到一条边u-v使得s-v,u-t.然后将链翻转得到一条哈密顿回路.

4. 如果该哈密顿回路长度已经为n,直接返回.否则在图上找到一个点与回路上的某个点相连,强行破环为链,链长++,返回2

证明,略.

```cpp
%:pragma GCC optimize(3)
#include<iostream>
#include<algorithm>
#include<cstring>
#include<cstdio>
#include<cmath>
#include<bitset>
#include<sstream>
#include<vector>
using namespace std;
const int MAXN=2000;
int n;
bitset<MAXN+10> G[MAXN+10];
int now[MAXN+10],sz;
bool a[MAXN+10],b[MAXN+10];
void addone(int x)
{
	a[x]=true;
	for(int i=1;i<=sz;++i)
	{
		if(G[x][now[i]])
		{
			rotate(now+1,now+i+1,now+sz+1);
			now[++sz]=x;break;
		}
	}
	for(int i=1;i<=n;++i)if(G[x][i])b[i]=true;
}
void dfs(int u)
{
	for(int i=1;i<=n;++i)
	{
		if(a[i]||!G[u][i])continue;
		now[++sz]=i;a[i]=true;dfs(i);break;
	}
}
void darkit()
{
	if(sz==n)return;
	dfs(now[sz]);reverse(now+1,now+sz+1);dfs(now[sz]);
	for(int i=1;i<n;++i)
		if(G[now[i+1]][now[1]]&&G[now[i]][now[sz]])
		{
			reverse(now+i+1,now+sz+1);
			break;
		}
	for(int i=1;i<=n;++i)if(!a[i]&&b[i]){addone(i);break;}
	darkit();
}
char s[10*MAXN+10],*p;
bool getint(int& v,char* &p)
{
	while((*p)&&!isdigit(*p))++p;
	if(!(*p))return false;
	v=0;
	while(isdigit(*p))v=v*10+(*p)-'0',++p;
	return true;
}
int main()
{
	scanf("%d\n",&n);
	for(int u=1,v;u<=n;++u)
	{
		gets(s);p=s;
		while(getint(v,p))G[u][v]=G[v][u]=true;
	}
	a[1]=true;now[sz=1]=1;
	darkit();
	for(int i=1;i<=n;++i)
	{
		if(now[i]==1)
		{
			reverse(now+1,now+i+1);
			reverse(now+i+1,now+n+1);
		}
	}
	for(int i=1;i<=n;++i)printf("%d ",now[i]);puts("1");
	return 0;
}
```

## 状压求简单图哈密顿回路数量

[CF 11 D](http://codeforces.com/problemset/problem/11/D)

设f[s][i]表示从s中编号最小的节点经过s中的点到i的哈密顿路径个数.

为什么只需要这些路径就够了呢,因为对于一个环,它总是可以这样拆的.

```cpp
#include<iostream>
#include<algorithm>
#include<cstring>
#include<cmath>
#include<cstdio>
using namespace std;
#define ll long long
const int MAXN=20;
int n,m,S;
bool G[MAXN+10][MAXN+10];
ll f[(1<<MAXN)+10][MAXN+10];
inline int bitcount(int x)
{
	int cnt=0;
	while(x){cnt+=(x&1);x>>=1;}
	return cnt;
}
inline int lowbit(int x){return x&(-x);}
ll ans;
int main()
{
	scanf("%d%d",&n,&m);S=(1<<n)-1;
	for(int i=1,u,v;i<=m;++i){scanf("%d%d",&u,&v);--u;--v;G[u][v]=G[v][u]=true;}
	for(int i=0;i<n;++i)f[1<<i][i]=1;
	for(int l=1;l<n;++l)
	{
		for(int i=0;i<=S;++i)
		{
			if(bitcount(i)^l)continue;
			for(int u=0;u<n;++u)
			{
				if(!f[i][u])continue;
				for(int v=0;v<n;++v)
				{
					if(((1<<v)<lowbit(i))||((1<<v)&i)||!(G[u][v]))continue;
					f[i^(1<<v)][v]+=f[i][u];
				}
			}
		}
	}
	for(int i=0;i<=S;++i)
	{
		if(bitcount(i)<3)continue;
		for(int u=0;u<n;++u)
		{
			if(!f[i][u])continue;
			for(int v=0;v<n;++v)
			{
				if(!(G[u][v])||(lowbit(i)!=(1<<v)))continue;
				ans+=f[i][u];
			}
		}
	}
	printf("%lld",ans>>1);
	return 0;
}
```
