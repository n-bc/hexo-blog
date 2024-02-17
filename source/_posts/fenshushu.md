<!-- wp:paragraph -->
<p>19世纪的时候，Moriz Stern（1858）与Achille Brocot（1860）发明了“一棵树”。据说，经由一些简单的规则而产生的这一棵树上，可以包含零以上所有的有理数。这棵树看起来大致这样：&nbsp;此题 列 对应 我们传统的行</p>
<!-- /wp:paragraph -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://bmh.coderlands.com/upload/image/20230301/20230301151853_99158.jpg" alt=""/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>你观察出规则了吗？</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>首先，它们在第一列放两个“分数”，第一个是0/1，代表0；第二个是1/0，代表无穷大。接着它们一列一列的产生这棵树，当它们要产生第k+1列的时候，就先把前k列所有的分数按照大小排成一列（假设有n个），在这些数之间会有n-1个间隔，那么第k+1列就准备产生n-1个数，其值的分子恰好是左右两个数的分子的和，分母是左右两个数的分母的和。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>例如，2/3，而它的2就是左边1/2的1和右边1/1的分子1相加的结果；而2/3的3，则是1/2的2加上1/1的分母1而得。 从这棵树中，我们可以看出，每个正的最简分数在这棵树中恰好出现一次，我们用字母“L”和“R”分别表示从树根（1/1）开始的一步“往左走”和“往右走”，则每一个数都可以由L和R组成的序列表示。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>例如，LRRL表示从1/1开始往左走一步到1/2，然后往右走到2/3，再往右走到3/4，最后往左走到5/7。我们可以把LRRL看作5/7的一种表示法。几乎每个正分数均有唯一的方法表示成一个由L和R组成的序列。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>给定一个分数，输出它的LR表示法。</p>
<!-- /wp:paragraph -->

<!-- wp:separator -->
<hr class="wp-block-separator has-alpha-channel-opacity"/>
<!-- /wp:separator -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">输入格式(Format Input)</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>有两个互为素数的正整数m和n（1&lt;=n,m&lt;=1000）</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">输出格式(Format Output)</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>对应的LR表示法</p>
<!-- /wp:paragraph -->

<!-- wp:separator -->
<hr class="wp-block-separator has-alpha-channel-opacity"/>
<!-- /wp:separator -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">输入样例(Sample Input) </h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>5 7</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">输出样例(Sample Output)</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>LRRL</p>
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
int n,m;
string ans;
void dfs(int l1,int l2,int r1,int r2)
{
	int a1=l1+r1;
	int a2=l2+r2;
	if(a1==n&amp;&amp;a2==m)	
	{
		cout&lt;&lt;ans;
		exit(0);
	}
	if(n*a2&lt;a1*m)
	{
		ans+='L';
		dfs(l1,l2,a1,a2);
	}
	if(n*a2>a1*m)
	{
		ans+='R';
		dfs(a1,a2,r1,r2);
	}
}
int main()
{
	cin>>n>>m;
	dfs(0,1,1,0); 
	return 0;
}</code></pre>
<!-- /wp:code -->
