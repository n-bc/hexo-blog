---
title: 单源最短路
---
<!-- wp:paragraph -->
<p>给出一个有向图，请输出从某一点出发到所有点的最短路径长度。</p>
<!-- /wp:paragraph -->

<!-- wp:separator -->
<hr class="wp-block-separator has-alpha-channel-opacity"/>
<!-- /wp:separator -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">输入格式(Format Input)</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>第一行包含三个整数N、M、S，分别表示点的个数、有向边的个数、出发点的编号。 接下来M行每行包含三个整数Fi、Gi、Wi，分别表示第i条有向边的出发点、目标点和长度(长度不会超过100)。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">输出格式(Format Output)</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>一行，包含N个用空格分隔的整数，其中第i个整数表示从点S出发到点i的最短路径长度（若S=i则最短路径长度为0，若从点S无法到达点i，则最短路径长度为-1）</p>
<!-- /wp:paragraph -->

<!-- wp:separator -->
<hr class="wp-block-separator has-alpha-channel-opacity"/>
<!-- /wp:separator -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">输入样例(Sample Input) </h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>4 6 1 1 2 2 2 3 2 2 4 1 1 3 5 3 4 3 1 4 4</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">输出样例(Sample Output)</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>0 2 4 3</p>
<!-- /wp:paragraph -->

<!-- wp:separator -->
<hr class="wp-block-separator has-alpha-channel-opacity"/>
<!-- /wp:separator -->

<!-- wp:paragraph -->
<p><strong>代码(Code)</strong></p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;bits/stdc++.h>
using namespace std;
struct point{
	int e,w;
}; 
vector&lt;point>head&#91;10010];
int n,m,s,dis&#91;10010],used&#91;10010];
int main()
{
	cin>>n>>m>>s;
	for(int i=1;i&lt;=m;i++)
	{
		int x,y,z;
		cin>>x>>y>>z;
		head&#91;x].push_back(point{y,z});
	}
	memset(dis,0x7f,sizeof(dis));
	dis&#91;s]=0;
	for(int i=1;i&lt;=n;i++)
	{
		int Min=1e9,k=0;
		for(int j=1;j&lt;=n;j++)
		{
			if(Min>dis&#91;j]&amp;&amp;used&#91;j]==0)
			{
				Min=dis&#91;j],k=j;
			}
		}
		if(Min==1e9)	break;
		used&#91;k]=1;
		for(int j=0;j&lt;head&#91;k].size();j++)
		{
			int v=head&#91;k]&#91;j].e;
			int va=head&#91;k]&#91;j].w;
			if(dis&#91;v]>dis&#91;k]+va)	dis&#91;v]=dis&#91;k]+va;
		}
	}
	for(int i=1;i&lt;=n;i++)
	{
		if(dis&#91;i]==0x7f7f7f7f)
		{
			cout&lt;&lt;-1&lt;&lt;" ";
		}
		else
		{
			cout&lt;&lt;dis&#91;i]&lt;&lt;" ";
		 } 
	}
	return 0;
}</code></pre>
<!-- /wp:code -->
