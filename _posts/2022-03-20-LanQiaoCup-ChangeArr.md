修改数组
时间限制: 1.0s 内存限制: 256.0MB 本题总分：20 分
【问题描述】
给定一个长度为 N 的数组 A = [A1, A2, · · · AN]，数组中有可能有重复出现的整数。
现在小明要按以下方法将其修改为没有重复整数的数组。小明会依次修改
A2, A3, · · · , AN。
当修改 Ai 时，小明会检查 Ai 是否在 A1 ～ Ai-1 中出现过。如果出现过，则小明会给 Ai 加上 1 ；如果新的 Ai 仍在之前出现过，小明会持续给 Ai 加 1 ，直到 Ai 没有在 A1 ～ Ai-1 中出现过。
当 AN 也经过上述修改之后，显然 A 数组中就没有重复的整数了。现在给定初始的 A 数组，请你计算出最终的 A 数组。
【输入格式】
第一行包含一个整数 N。
第二行包含 N 个整数 A1, A2, · · · , AN 。
【输出格式】
输出 N 个整数，依次是最终的 A1, A2, · · · , AN。


【样例输入】
5
2 1 1 3 4
【样例输出】
2 1 3 4 5

【评测用例规模与约定】
对于 80% 的评测用例，1 ≤ N ≤ 10000。
对于所有评测用例，1 ≤ N ≤ 100000，1 ≤ Ai ≤ 1000000。

解题思路

bool标记每次+1很容易就t了（如果有N个数，全都为N，那么这是O(n^2/2）的复杂度，当n=1e5时就已经超时了）。这题可以巧妙地利用并查集。 我们初始化i的父亲为i，然后依次遍历输入的数组，使a[i] = getf(a[i]),再令f(a[i]) = getf(a[i]+1)即可。

假如我们连续输入1，2,1，第一次输入1，a[1] = getf(1) = 1,更新f[1] = getf(a[1]+1) = 2； 第二次输入  输入2，a[2] = getf(2) =2,更新f[2] = getf(a[2]+1） = 3，第三次 再输入1，a[3] = getf(1) = getf(2） = 3， 这时候a[3]便等于3了，而这种 查 的时间复杂度仅为O( logn)。  很巧妙 好好体会。

整体时间复杂度O(n*logn*logn)。 

```c++
#include<iostream>
#include<bits/stdc++.h>
#define MaxNum 100001
using namespace std;
int f[MaxNum], a[MaxNum];

int getf(int x)
{
	return f[x] = f[x] == x? x:getf(f[x]);
}


int main()
{
	int n;
	scanf("%d", &n);
	for(int i = 1; i <= MaxNum; i++)
	{
		f[i] = i;
	}
	for(int i = 0; i < n; i++)
	{
		scanf("%d",&a[i]);
		a[i] = getf(a[i]);
		f[a[i]] = getf(a[i] + 1);  // 类似于union操作,根为下一个满足f[x] == x的x 
	}
	for(int i = 0 ; i < n; i++)
	{
		cout << a[i];
		if(i != n-1)
		{
			cout << " ";
		}
	}
	return 0;
}
```



————————————————
原文链接：https://blog.csdn.net/weixin_42765557/article/details/89480557