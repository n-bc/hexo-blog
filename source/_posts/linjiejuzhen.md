---
title: C++：邻接矩阵存图
date: 2023-12-31
---
<!-- wp:paragraph -->
<p>给定n个点, m条单向边&nbsp;&nbsp;n&lt;=1000, m &lt;= 100000</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>有k个询问，询问x出去的所有边及其权值，如果有多条边，终点编号小的先输出，具体见样例</p>
<!-- /wp:paragraph -->

<!-- wp:separator -->
<hr class="wp-block-separator has-alpha-channel-opacity"/>
<!-- /wp:separator -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">输入格式(Format Input)</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>第一行输入两个整数n和m，表示有n个点和m条边。 接下来输入m行，每行三个整数x y z，表示x到y有一条权值为z的单向边。如果两个点之间有多条边，保留权值最小的一条。 输入一个数字k，表示有k个询问（k&lt;=n）。 接下来输入k行，每行输入一个整数x（x表示节点编号）。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">输出格式(Format Output)</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>对于每一个询问x，输入与x相连的边，每条边占一行，对于每条边先输出终点编号，再输出边权，中间用空格隔开。</p>
<!-- /wp:paragraph -->

<!-- wp:separator -->
<hr class="wp-block-separator has-alpha-channel-opacity"/>
<!-- /wp:separator -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">输入样例(Sample Input) </h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>4 5 </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>1 2 5 </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>1 3 4 </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>2 4 3 </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>1 4 8 1 3 3 </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>2 </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> 2</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">输出样例(Sample Output)</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>2 5 3 3 4 8 4 3</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>前项星写法：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;bits/stdc++.h>
using namespace std;
int n,m,k,cnt=0;//cnt表示第i条边，默认为0。 k:几组查询 
int last&#91;1010];//last&#91;i]代表i后的第一个边。
int nxt&#91;1010];//nxt&#91;i]代表第i条边的下一条边。
int w&#91;1010];//w&#91;i]代表第i条边的权值。
int ed&#91;1010];//ed&#91;i]表示第i条边的“终点”。
void edge(int x,int y,int z)//新增一条从x至y，边权为z的边。
{
	cnt++;//此乃第i条边！
	ed&#91;cnt]=y,w&#91;cnt]=z;//i条边终点为y,边权为z。
	//前插法 将数据从“头 ”插入 。 
	nxt&#91;cnt]=last&#91;x];//i的下一条边为第x（起点）点后的第一条边。 
	last&#91;x]=cnt;//x（起点）点后的第一条边为第i条边。 
	//注意！先让i的下一条边为第x（起点）点后的第一条边，再让x（起点）点后的第一条边为第i条边。这样才不会将图“断掉 ”。 
}
int main()
{
	cin>>n>>m;
	for(int i=1;i&lt;=m;i++)
	{
		int x,y,z;
		cin>>x>>y>>z;
		edge(x,y,z);//新增一条从x至y，边权为z的边。 
	}
	cin>>k;
	for(int i=1;i&lt;=k;i++)
	{
		int x;
		cin>>x;//键入要查询的节点。 
		for(int j=last&#91;x];j;j=nxt&#91;j])	//设j为 x后的第一条边。如果j!=0，就一直运行。这遍循环后，j来到j+1条边。 
		{
			cout&lt;&lt;ed&#91;j]&lt;&lt;" "&lt;&lt;w&#91;j]&lt;&lt;endl;	//输出终点与边权。 
		}
	}
	return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>但由于本人太菜了?，只会前插法，所以还是用暴力点的法子吧。这法子存储的是点，上边的是边。</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;bits/stdc++.h>
using namespace std;
int n,m,k;
int g&#91;1001]&#91;1001];
int main()
{
	cin>>n>>m;
	memset(g,-1,sizeof(g));//初始值全列为-1，由于本体无负权边，so，无伤大雅。
	for(int i=1;i&lt;=m;i++)
	{
		int x,y,z;
		cin>>x>>y>>z;
		if(g&#91;x]&#91;y]==-1) g&#91;x]&#91;y]=z;//如果直接min，g&#91;x]&#91;y]永远为-1，so，特判一下。
		else g&#91;x]&#91;y]=min(g&#91;x]&#91;y],z);
	}
	cin>>k;
	for(int i=1;i&lt;=k;i++)
	{
		int x;
		cin>>x;
		for(int j=1;j&lt;=n;j++)//快乐地循环n次。
		{
			if(g&#91;x]&#91;j]!=-1)//有边权！！！
			{
				cout&lt;&lt;j&lt;&lt;" "&lt;&lt;g&#91;x]&#91;j]&lt;&lt;endl;//快乐地输出
			}
		}
	}
	return 0;
}</code></pre>
<!-- /wp:code -->
