---
layout: post
title: HelloWorld
date: 2018-02-08 12:14:0 +0800
categories: technology
tags: 数据结构
img: 
---

# 树分块

感觉我已经越来越懒了啊...

于是就放一道题:

### [A. Queries on the Tree](http://codeforces.com/gym/100589/problem/A)

然后贴一份代码.

```cpp
#include<iostream>
#include<vector>
#include<algorithm>
#include<cstring>
#include<cmath>
#include<cstdio>
using namespace std;
#define int long long
const int V=111111;
const int E=222222;
const int MAXB=520;
int rd;char ch;
inline int read()
{
	while(!isdigit(ch=getchar()));
	rd=ch-'0';
	while(isdigit(ch=getchar()))rd=rd*10-'0'+ch;
	return rd;
}
int n,m,B;
int fir[V],nxt[E],to[E],tote;
inline void adde(int u,int v)
{
	to[++tote]=v;nxt[tote]=fir[u];fir[u]=tote;
	to[++tote]=u;nxt[tote]=fir[v];fir[v]=tote;
}
int f[V],sz[V],dep[V],id[V];
void dfs(int u)
{
	dep[u]=dep[f[u]]+1;
	for(int i=fir[u],v;i;i=nxt[i])
	{
		if((v=to[i])==f[u])continue;
		f[v]=u;dfs(v);
	}
}
bool cmp(int x,int y){return dep[x]>dep[y];}
int rec[V],ed,in[V],tot,cnt[MAXB][V],up[MAXB],s[V],w[V];
void pack(int u)
{
	in[u]=tot;++cnt[tot][dep[u]];
	for(int i=fir[u],v;i;i=nxt[i])
		if((v=to[i])!=f[u]&&!in[v])pack(v);
}
int calc(int u)
{
	int res=w[dep[u]]+s[u];
	for(int i=fir[u],v;i;i=nxt[i])
		if((v=to[i])!=f[u]&&in[v]==in[u])res+=calc(v);
	return res;
}
signed main()
{
	n=read();m=read();B=sqrt(n);
	for(int i=1;i<n;++i)adde(read(),read());
	dep[0]=-1;dfs(1);
	for(int i=1;i<=n;++i)id[i]=i;
	sort(id+1,id+n+1,cmp);
	for(int k=1,u,sum;k<=n;++k)
	{
		sum=ed=0;sz[u=id[k]]=1;
		for(int i=fir[u],v;i;i=nxt[i])if((v=to[i])!=f[u])sz[u]+=sz[v];
		for(int i=fir[u],v;i;i=nxt[i])
		{
			if((v=to[i])==f[u])continue;
			sum+=sz[v];rec[++ed]=v;
			if(sum>=B)
			{
				sz[u]-=sum;up[++tot]=u;sum=0;
				for(int j=1;j<=ed;++j)pack(rec[j]);
				ed=0;
			}
		}
	}
	++tot;pack(1);
	for(int i=1,u;i<tot;++i)
	{
		u=in[up[i]];
		for(int j=1;j<=n;++j)cnt[u][j]+=cnt[i][j];
	}
	int op,x,y;
	while(m--)
	{
		op=read();x=read();
		if(op&1)
		{
			w[x]+=(y=read());
			for(int i=1;i<tot;++i)
				s[up[i]]+=y*cnt[i][x];
		}
		else printf("%lld\n",calc(x));
	}
	return 0;
}
```
