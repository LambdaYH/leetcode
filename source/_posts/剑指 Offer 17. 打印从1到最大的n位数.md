---
title: 剑指 Offer 17. 打印从1到最大的n位数
date: 2021-08-30 20:12:54 +0800
categories: leetcode
mathjax: false

---

#### [剑指 Offer 17. 打印从1到最大的n位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)



不考虑大数的情况

```c++
class Solution {
public:
    vector<int> printNumbers(int n) {
        vector<int> ret;
        int maxNum = pow(10, n);
        for(int i = 1; i < maxNum; ++i)
            ret.push_back(i);
        return ret;
    }
};
```



##### 考虑大数的情况



需要使用字符串来表示数字

首先通过回溯，对于特定的位数，衔接上0~9

再进行去除前导0，设字符串无前导0的起始点为start，n为3时

则

1~9时，start=2

10~99时，start = 1

100~999时，start=0



综上可以得出start=n-(9的个数)

所以当碰到9时，增加9的个数，而但start = n - nine时，这时的所有位都是9，使start-1，表示要进位了

```c++
class Solution {
public:
	vector<string> printNumbers(int n) {
		vector<string> ret;
		string tmp;
		int start = n - 1;
		backTrack(ret, n, 0, tmp, start);
		return ret;
	}
private:
	void backTrack(vector<string>& ret, int n, int nine, string& tmp, int& start)
	{
		if (n == tmp.size())
		{
			auto res = tmp.substr(start);
			if(res != "0")
				ret.push_back(res);
			if (start == n - nine)  // 之所以在这里要用引用的形式，是因为根据回溯的顺序，他数字是依次递增的。如果在完成遍历0009后开始便利0010,那么如果不是引用，这时候传递的start依旧是之前的，因为变化是从返回前产生的
				--start;
			return;
		}
		for (int i = 0; i <= 9; ++i)
		{
			tmp += (char)(i + '0');
			if (i == 9)
				nine += 1;
			backTrack(ret, n, nine, tmp, start);
			tmp.pop_back();
		}
	}
};
```

