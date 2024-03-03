---
title: 最小生成树
date: 2024-03-03 17:20:05
---



**树：没有环的图**

**在图中找一个树：权值仅可能小，并且包含图中所有点<img src="/Users/cbwt/Desktop/高蔚713班主任 2024-02-02 08.13.06.png" alt="高蔚713班主任 2024-02-02 08.13.06"  />**



> 生成树：一个有n个结点的连通图的生成树是原图的极小连通子图，包含原图中的所有n个结点，并且有保持图连通的最少的边。
>
> 最小生成树：生成树中权值最小的一种方案。
>
> 给定一个无向图，请输出最小生成树的权值。
>
> 存在重边









**第一种方法：考虑边，克鲁斯卡尔发明（并查集）（Kruskal算法）**

**1.给边权排序 2 <del>2</del> 2 3 <del>3</del><del>  4</del>**

**2.考虑每条边的可能性**

```
#include<bits/stdc++.h>
using namespace std;
//克鲁斯卡尔
int n,m,used[400001],num,ans;
struct p{
	int x,y,z;//起点终点，权值
}a[400001];
int find(int x)
{
	return used[x]=used[x]==x?x:find(used[x]);
}
bool cmp(p x,p y)
{
	return x.z<y.z;//比权值
}
int main()
{
	cin>>n>>m;
	for(int i=1;i<=m;i++)
	{
		cin>>a[i].x>>a[i].y>>a[i].z;//输入
	}
	sort(a+1,a+1+m,cmp);
	//比较每条边的“老大”是否是同一个人。同一个人，即边在统一组织，不能纳入。
	for(int i=1;i<=n;i++)
		used[i]=i;
	for(int i=1;i<=m;i++)
	{
		int u=find(a[i].x);
		int v=find(a[i].y);
		if(u!=v)//“老大”不一样，能合并。
		{
			used[u]=v;
			ans+=a[i].z;
			num++;
			if(num==n-1)
			{
				cout<<ans;
				break;
			}
		}
	}
	return 0;
}
```

**第二种情况：考虑点，一个点能够连接的最小权值边，并考虑可能性（Prime算法）**

```
#include<bits/stdc++.h>
using namespace std;
//Prime
struct point{
	int e,w;
};
vector<point>head[100000];
int n,m,x,y,z,num,ans;
int dis[1000000],used[100000];
int main()
{
	cin>>n>>m;
	for(int i=1;i<=m;i++)
	{
		cin>>x>>y>>z;
		head[x].push_back(point{y,z});
		head[y].push_back(point{x,z});
	}
	memset(dis,0x7f,4*100000);
	dis[1]=0;
	for(int i=1;i<=n;i++)
	{
		int Min=1e9,k;
		for(int j=1;j<=n;j++)
		{
			if(used[j]==0&&Min>dis[j])
			{
				Min=dis[j];
				k=j;
			}
		}
		if(k==0)
		{
			cout<<-1;
			return 0;
		}
		used[k]=1;
		ans+=dis[k];
		num++;
		if(num==n)
		{
			cout<<ans;
			return 0;
		}
		for(int j=0;j<head[k].size();j++)
		{
			int v=head[k][j].e;
			int va=head[k][j].w;
			if(dis[v]>va)
			{
				dis[v]=va;

			}
		}
	}
	return 0;
}
```

