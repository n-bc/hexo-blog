---
title: Hoof, Paper, Scissors【USACO 2017 January Contest, Bronze】
---
<!-- wp:heading -->
<h2 class="wp-block-heading">题目描述(Description)</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><br>You have probably heard of the game "Rock, Paper, Scissors". The cows like to play a similar game they call "Hoof, Paper, Scissors".</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The rules of "Hoof, Paper, Scissors" are simple. Two cows play against each-other. They both count to three and then each simultaneously makes a gesture that represents either a hoof, a piece of paper, or a pair of scissors. Hoof beats scissors (since a hoof can smash a pair of scissors), scissors beats paper (since scissors can cut paper), and paper beats hoof (since the hoof can get a papercut). For example, if the first cow makes a "hoof" gesture and the second a "paper" gesture, then the second cow wins. Of course, it is also possible to tie, if both cows make the same gesture.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Farmer John watches in fascination as two of his cows play a series of N games of "Hoof, Paper, Scissors" (1≤N≤100). Unfortunately, while he can see that the cows are making three distinct types of gestures, he can't tell which one represents "hoof", which one represents "paper" and which one represents "scissors" (to Farmer John's untrained eye, they all seem to be variations on "hoof"...)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Not knowing the meaning of the three gestures, Farmer John assigns them numbers 1, 2, and 3. Perhaps gesture 1 stands for "hoof", or maybe it stands for "paper"; the meaning is not clear to him. Given the gestures made by both cows over all N games, please help Farmer John determine the maximum possible number of games the first cow could have possibly won, given an appropriate mapping between numbers and their respective gestures.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>你可能听说过“石头、布、剪刀”游戏。奶牛喜欢玩一种类似的游戏，他们称之为“蹄子、布、剪刀”。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>游戏的规则很简单。两头母牛互相玩耍。他们都数到三，然后每个人同时做一个手势，表示一只蹄子、一张纸或一把剪刀。蹄子打败剪刀（因为蹄子可以打碎剪刀），剪刀打败纸（因为剪刀可以剪纸），纸打败蹄子（因为纸包裹蹄子）。例如，如果第一头牛做出“蹄子”手势，第二头牛做出“纸”手势，那么第二头牛获胜。当然，如果两头母牛做出相同的姿势，也可以打平局。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>农夫约翰着迷地看着他的两只母牛玩一系列的“蹄子、布、剪刀”游戏（1）≤N≤100). 不幸的是，虽然他能看到奶牛在做三种不同类型的手势，但他不知道哪一种代表“蹄”，哪一种代表“纸”，哪一种代表“剪刀”（在农夫约翰未经训练的眼里，它们似乎都是“蹄”的变体……）</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>由于不知道这三个手势的意思，农夫约翰给他们分配了数字1、2和3。可能手势1代表“蹄子”，也可能代表“纸”；他的意思不清楚。考虑到两头母牛在所有N场比赛中做出的手势，请帮助农夫约翰确定第一头母牛可能赢得的最大游戏数，给出数字和它们各自手势之间的适当映射。</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading">输入格式(Format Input)</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The first line of the input file contains N.<br>Each of the remaining N lines contain two integers (each 1, 2, or 3), describing a game from Farmer John's perspective.<br>输入文件的第一行包含N。<br>剩下的N行中的每一行都包含两个整数（分别为1、2或3），从农夫约翰的角度描述了一场游戏。<br>输出格式(Format Output)<br>Print the maximum number of games the first of the two cows could possibly have won.<br>打印两头母牛中第一头可能赢得的最大游戏数。</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading">输入样例(Sample Input)</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><br>5<br>1 2<br>2 2<br>1 3<br>1 1<br>3 2</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading">输出样例(Sample Output)</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><br>2</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading">说明/提示(Hint)</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><br>One solution (of several) for this sample case is to have 1 represent "scissors", 2 represent "hoof", and 3 represent "paper". This assignment gives 2 victories to the first cow ("1 3" and "3 2"). No other assignment leads to more victories.<br>对于这个示例案例，一种解决方案是1代表“剪刀”，2代表“蹄子”，3代表“纸”。这项任务给第一头牛两次胜利（“1 3”和“3 2”）。没有其他任务能带来更多的胜利。</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;bits/stdc++.h&gt;
using namespace std;
int n,ans1,ans2;
int fir&#91;1001],sec&#91;1001];
int main()
{
    cin&gt;&gt;n;
    for(int i=1;i&lt;=n;i++)
    {
        cin&gt;&gt;fir&#91;i]&gt;&gt;sec&#91;i];
    }
    for(int i=1;i&lt;=n;i++)
    {
        if(fir&#91;i]-sec&#91;i]==-1||fir&#91;i]-sec&#91;i]==2)
        {
            ans1++;
        }
        if(fir&#91;i]-sec&#91;i]==1||fir&#91;i]-sec&#91;i]==-2)
        {
            ans2++;
        }
    }
    cout&lt;&lt;max(ans1,ans2);
    return 0;
}</code></pre>
<!-- /wp:code -->
