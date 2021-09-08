---
title: 剑指 Offer 43. 1～n 整数中 1 出现的次数
date: 2021-06-30 16:12:37 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 43. 1～n 整数中 1 出现的次数](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)

##### brute force

但是超时了
```c++
class Solution {
public:
    int countDigitOne(int n) {
        int ret = 0;
        for(int i = 1; i <= n; ++i)
        {
            int tmp = i;
            while(tmp)
            {
                ret += (tmp % 10 == 1 ? 1 : 0);
                tmp /= 10;
            }
        }
        return ret;
    }
};
```

##### 用dp超内存了


##### 数学方法

（企及不到的境界）（又称为数位dp)

```
class Solution {
public:
    int countDigitOne(int n) {
        int ret = 0;
        int high = n / 10, cur = n % 10, low = 0;
        long digit = 1;
        while(high || cur) // 注意这里是cur和high，当high非0时，表示还没到最高位，当high为0时，如果cur为0，则这一位不可能为1，如果cur不为0，那么下一个循环cur为0，都可以终止
        {
            if(cur == 0)
                ret += high * digit;
            else if(cur == 1)
                ret += high * digit + 1 + low;
            else
                ret += (high + 1) * digit;
            low += cur * digit;
            cur = high % 10;
            high /= 10;
            digit *= 10;
        }
        return ret;
    }
};
```

所求的是每一位1出现的次数，所有位加起来那就是总和了。

将当前位想象成密码锁

1. 当前位为0，那么将这一位固定为1后，掰动其他位所能生成的组合的数量将会是`高位*数位`，例如，`2402`中的第三位为0，将这一位固定为1后，由于生成的数必须小于`2402`，所以上限将等于`2319`，可以发现高位是减了1的，则总数就是`0010~2319`，其他数有`000~239`种变化。
2. 当前位为1，那么这一位固定为1后，可以为所欲为，例如，`2412`，对于第三位范围就是`0000~2412`范围就是`000~242`，也就是`高位*数位+低位+1`
3. 当前位为其他，那么把这一位固定为1后，范围就是这一位被压制为1后的值，例如`2432`，其范围就是`0000~2419`，最后范围就是`000~249`，也就是`(高位+1) * 数位`。
