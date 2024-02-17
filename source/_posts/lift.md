---
title:洛谷P1135 奇怪的电梯
---
<!-- wp:heading -->
<h2 class="wp-block-heading"><strong>题目描述(Description)</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><br>有一天我做了一个梦，梦见了一种很奇怪的电梯。大楼的每一层楼都可以停电梯，而且第i层楼(1≤i≤N)上有一个数字Ki(0≤Ki≤N)。电梯只有四个按钮：开，关，上，下。上下的层数等于当前楼层上的那个数字。当然，如果不能满足要求，相应的按钮就会失灵。例如：3,3,1,2,5代表了Ki(K1=3,K2=3,…)，从1楼开始。在1楼，按“上”可以到4楼，按“下”是不起作用的，因为没有−2楼。那么，从A楼到B楼至少要按几次按钮呢？</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading"><strong>输入格式(Format Input)</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><br>共二行。<br>第一行为3个用空格隔开的正整数，表示N,A,B(1≤N≤200, 1≤A,B≤N)<br>第二行为N个用空格隔开的非负整数，表示Ki。<br>输出格式(Format Output)<br>一行，即最少按键次数,若无法到达，则输出−1。</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading"><strong>输入样例(Sample Input)</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><br>5 1 5<br>3 3 1 2 5</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading"><strong>输出样例(Sample Output)</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><br>3</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading"><strong>解析</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><br>这道题其实不难，就是一个深搜，些许判断就行。</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading"><strong>代码</strong></h2>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;bits/stdc++.h&gt;
using namespace std;
int n,y,b,a&#91;1001];
bool used&#91;1001];
int ans=1e9;
void dfs(int step,int last)
{
    if(last==b)
    {
        ans=min(ans,step);
        return;
    }
    if(step&gt;ans)    return;
    if(last+a&#91;last]&lt;=n&amp;&amp;used&#91;last+a&#91;last]]==0)
    {
        used&#91;last+a&#91;last]]=1;
        dfs(step+1,last+a&#91;last]);
        used&#91;last+a&#91;last]]=0;
    }
    if(last-a&#91;last]&gt;=1&amp;&amp;used&#91;last+a&#91;last]]==0)
    {
        used&#91;last-a&#91;last]]=1;
        dfs(step+1,last-a&#91;last]);
        used&#91;last-a&#91;last]]=0;
    }
 } 
int main()
{
    cin&gt;&gt;n&gt;&gt;y&gt;&gt;b;
    for(int i=1;i&lt;=n;i++)
    {
        scanf("%d",&amp;a&#91;i]);
    }
    dfs(0,y);
    if(ans==1e9)    cout&lt;&lt;-1;
    else cout&lt;&lt;ans;
    return 0;
 }
</code></pre>
<!-- /wp:code -->
