---
layout: post
title: Eulerian Path
date: 2017-10-29 10:15:0 +0800
categories: technology
tags: 图论
img: 
---
Euler is Euler

# 欧拉迹

## Definition

一笔画问题...

## 如何求

[UOJ117](http://uoj.ac/problem/117)

解释什么的...先占个坑吧...~~想必每次占坑都是永远不会填的~~

好的吧,然后就是

```cpp
#include<iostream>
#include<algorithm>
#include<cstring>
#include<cstdio>
#include<cmath>
using namespace std;
const int MAXN=1000000;
const int MAXM=2000000;
int t;
struct Edge{int u,v,id;};
struct Solver1
{
	int n,m,fir[MAXN+10],nxt[MAXM+10],tote,d[MAXN+10],in[MAXN+10],ans[MAXM+10],ed;
	Edge edges[MAXM+10];
	bool vis[MAXM+10];
	void adde(int u,int v,int id)
	{
		edges[++tote]=(Edge){u,v,id};
		nxt[tote]=fir[u];fir[u]=tote;
	}
	void init()
	{
		memset(fir,0,sizeof fir);
		memset(vis,0,sizeof vis);
		tote=1;ed=0;
	}
	int find(int a){return (in[a]==a)?a:(in[a]=find(in[a]));}
	void hb(int a,int b){in[find(a)]=find(b);}
	void dfs(int u)
	{
		for(int& i=fir[u];i;i=nxt[i])
		{
			Edge& e=edges[i];
			if(vis[abs(e.id)])continue;
			vis[abs(e.id)]=true;
			dfs(e.v);ans[++ed]=e.id;
		}
	}
	void solve()
	{
		init();scanf("%d%d",&n,&m);
		for(int i=1;i<=n;++i)in[i]=i;
		for(int i=1,u,v;i<=m;++i)
		{
			scanf("%d%d",&u,&v);
			adde(u,v,i);adde(v,u,-i);
			++d[u];++d[v];hb(u,v);
		}
		bool flag=true;int cur=-1;
		for(int i=1;i<=n;++i)if(d[i]&1){flag=false;break;}
		for(int i=1;i<=n;++i)
		{
			if(!fir[i])continue;
			if(cur==-1)cur=find(i);
			else if(cur!=find(i)){flag=false;break;}
		}
		if(!flag){puts("NO");return;}
		else puts("YES");
		for(int i=1;i<=n;++i)if(d[i]){dfs(i);break;}
		for(int i=ed;i;--i)printf("%d ",ans[i]);
	}
};
struct Solver2
{
	int n,m,fir[MAXN+10],nxt[MAXM+10],tote,in[MAXN+10],d[MAXN+10],ans[MAXM+10],ed;
	Edge edges[MAXM+10];
	bool vis[MAXM+10];
	void adde(int u,int v,int id)
	{
		edges[++tote]=(Edge){u,v,id};
		nxt[tote]=fir[u];fir[u]=tote;
	}
	void init()
	{
		memset(fir,0,sizeof fir);
		memset(vis,0,sizeof vis);
		tote=1;ed=0;
	}
	int find(int a){return (in[a]==a)?a:(in[a]=find(in[a]));}
	void hb(int a,int b){in[find(a)]=find(b);}
	void dfs(int u)
	{
		for(int& i=fir[u];i;i=nxt[i])
		{
			Edge& e=edges[i];
			if(vis[e.id])continue;
			vis[e.id]=true;
			dfs(e.v);ans[++ed]=e.id;
		}
	}
	void solve()
	{
		init();scanf("%d%d",&n,&m);
		for(int i=1;i<=n;++i)in[i]=i;
		for(int i=1,u,v;i<=m;++i)
		{
			scanf("%d%d",&u,&v);adde(u,v,i);
			++d[u];--d[v];hb(u,v);
		}
		bool flag=true;int cur=-1;
		for(int i=1;i<=n;++i)if(d[i]){flag=false;break;}
		for(int i=1;i<=n;++i)
		{
			if(!fir[i])continue;
			if(cur==-1)cur=find(i);
			else if(cur!=find(i)){flag=false;break;}
		}
		if(!flag){puts("NO");return;}
		else puts("YES");
		for(int i=1;i<=n;++i)if(fir[i]){dfs(i);break;}
		for(int i=ed;i;--i)printf("%d ",ans[i]);
	}
};
Solver1 qaq;
Solver2 qwq;
int main()
{
	scanf("%d",&t);
	if(t&1)qaq.solve();
	else qwq.solve();
	return 0;
}
```
