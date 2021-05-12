---
title: 4. Median of Two Sorted Arrays
date: 2021-03-05 21:44:00 +0800
categories: leetcode
---
#### [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)
```c++
class Solution
{
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2)
    {
        int m = nums1.size(), n = nums2.size();
        int left, right;
        if (m > n)
        {
            swap(nums1, nums2);
            swap(m, n);
        }
        if(m==0)
        {
            if(n % 2 == 1)
            {
                return nums2[n / 2];
            }else
            {
                return (nums2[n / 2] + nums2[n / 2 - 1]) / 2.0;
            }
        }
        int imin = 0, imax = m;
            

        while (imin <= imax)
        {
            int i = (imin + imax) / 2, j = (m + n + 1) / 2 - i;
            if (i > 0 && (nums1[i - 1] > nums2[j]))
            {
                imax = i - 1;
            }
            else if (i < m && (nums2[j - 1] > nums1[i]))
            {
                imin = i + 1;
            }
            else
            {
                if (i == 0)
                {
                    left = nums2[j - 1];
                }
                else if (j == 0)
                {
                    left = nums1[i - 1];
                }
                else
                {
                    left = max(nums1[i - 1], nums2[j - 1]);
                }

                if (i == m)
                {
                    right = nums2[j];
                }
                else if (j == n)
                {
                    right = nums1[i];
                }
                else
                {
                    right = min(nums1[i], nums2[j]);
                }
                if ((m + n) % 2 == 1)
                {
                    return left;
                }
                else
                {
                    return (left + right) / 2.0;
                }
            }
        }

        return 0;
    }
};
```
---
title: 4. Median of Two Sorted Arrays
date: 2021-03-05 21:44:00 +0800
categories: leetcode
---
#### [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)
```c++
class Solution
{
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2)
    {
        int m = nums1.size(), n = nums2.size();
        int left, right;
        if (m > n)
        {
            swap(nums1, nums2);
            swap(m, n);
        }
        if(m==0)
        {
            if(n % 2 == 1)
            {
                return nums2[n / 2];
            }else
            {
                return (nums2[n / 2] + nums2[n / 2 - 1]) / 2.0;
            }
        }
        int imin = 0, imax = m;
            

        while (imin <= imax) // 可以相等，表为0
        {
            int i = (imin + imax) / 2, j = (m + n + 1) / 2 - i;
            if (i > 0 && (nums1[i - 1] > nums2[j]))   // 本来是需要i>0 && j < n，但是由于满足n >= m，当i > 0时，j = (m + n + 1) / 2 - i <= (m + n + 1) / 2 <= (m + n + 1) / 2 <= m + 1/2 < m            {
                imax = i - 1;
            }
            else if (i < m && (nums2[j - 1] > nums1[i])) // j > 0 && i < m, 同上证明
            {
                imin = i + 1;
            }
            else
            {
                // 几种边缘情况处理
                if (i == 0)
                {
                    left = nums2[j - 1];
                }
                else if (j == 0)
                {
                    left = nums1[i - 1];
                }
                else
                {
                    left = max(nums1[i - 1], nums2[j - 1]);
                }

                if (i == m)
                {
                    right = nums2[j];
                }
                else if (j == n)
                {
                    right = nums1[i];
                }
                else
                {
                    right = min(nums1[i], nums2[j]);
                }
                if ((m + n) % 2 == 1)
                {
                    return left;
                }
                else
                {
                    return (left + right) / 2.0;
                }
            }
        }

        return 0;
    }
};
```
