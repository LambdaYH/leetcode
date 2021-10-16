---
title: 406. Queue Reconstruction by Height
date: 2021-04-15 11:23:09 +0800
categories: leetcode
---
#### [406. Queue Reconstruction by Height](https://leetcode.com/problems/queue-reconstruction-by-height/)

##### O(32n) 解法
```c++
class Solution {
public:
    vector<vector<int>> reconstructQueue(vector<vector<int>>& people) {
        sort(people.begin(), people.end(), [](vector<int>& p1, vector<int>& p2)
             {
                 return p1[0] > p2[0] || (p1[0] == p2[0] && p1[1] < p2[1]); 
             });
        vector<vector<int>> ret;
        for(auto& p : people)
        {
            ret.insert(ret.begin() + p[1], p);
        }
        return ret;
    }
};
```

先插入最高的人，最高的人组成的子序列所排列的顺序一定是由其K所决定的，当插入第二大的序列后，他不会影响第一大的序列，且仅仅由其本身和比他的序列影响，由其相对位置插入，可知，当为0时，就插到比他大的0前面，为1时，就插到比他大的1前面，比他大的那个往后移一位

结合[explaination](https://leetcode.com/problems/queue-reconstruction-by-height/discuss/89359/Explanation-of-the-neat-Sort%2BInsert-solution)
```
People are only counting (in their k-value) taller or equal-height others standing in front of them. So a smallest person is completely irrelevant for all taller ones. And of all smallest people, the one standing most in the back is even completely irrelevant for everybody else. Nobody is counting that person. So we can first arrange everybody else, ignoring that one person. And then just insert that person appropriately. Now note that while this person is irrelevant for everybody else, everybody else is relevant for this person - this person counts exactly everybody in front of them. So their count-value tells you exactly the index they must be standing.

So you can first solve the sub-problem with all but that one person and then just insert that person appropriately. And you can solve that sub-problem the same way, first solving the sub-sub-problem with all but the last-smallest person of the subproblem. And so on. The base case is when you have the sub-...-sub-problem of zero people. You're then inserting the people in the reverse order, i.e., that overall last-smallest person in the very end and thus the first-tallest person in the very beginning. That's what the above solution does, Sorting the people from the first-tallest to the last-smallest, and inserting them one by one as appropriate.
```

最后一个人的位置不会影响前面的人，但前面人的位置将影响到最后一个人，因此最后一个人的k必定表示其绝对位置，将其划分为一堆的子问题，每个子问题在解决时都先忽略子问题中最小的的那个数，那个数在所有其他数排列完后再插入那个绝对的位置。
依此，则从最大数开始排起，后面插入的数对于先前的序列来说必定是插入其的K位置，不断扩大子问题，往复，直到整个序列往复。最小的数插入到其的K位置。

中心思想：最小的数的k必定表示其在结果中的绝对位置，抛开这个最小的数，生成一个子问题。再抛开子问题中最小的数，生成一个子-子问题......
