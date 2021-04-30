---
title: 6. ZigZag Conversion
date: 2021-03-08 21:32:38 +0800
categories: leetcode
---
#### [6. ZigZag Conversion](https://leetcode.com/problems/zigzag-conversion/)
```c++
class Solution
{
public:
    string convert(string s, int numRows)
    {
        int size = s.size();
        if (numRows == 1)
        {
            return s;
        }
        int col = size / (numRows + numRows - 2);
        int addon = size - col * (numRows + numRows - 2);
        string result = "";
        int location = 0;
        for (size_t i = 0; i < numRows; ++i)
        {
            int bias;
            if (i == numRows - 1)
            {
                int temp = col + (addon >= numRows ? 1 : 0);
                for (int i = 0; i < temp; ++i)
                {
                    result += string(1, s[location + i*(numRows+numRows-2)]);
                }
                ++location;
                continue;
            }
            else if (i == 0)
            {
                int temp = col + (addon ? 1 : 0);
                for (int i = 0; i < temp; ++i)
                {
                    result += string(1, s[location + i * (numRows + numRows - 2)]);
                }
                ++location;
                continue;
            }
            else if (addon >= 2 * numRows - 2 - (i - 1))
            {
                bias = 2;
            }
            else if (addon >= i + 1)
            {
                bias = 1;
            }
            else
            {
                bias = 0;
            }
            int temp = col + col + bias;
            for (int i = 0; i < temp; ++i)
            {
                if(i%2==0)
                    result += string(1, s[location + (i/2) * (numRows + numRows - 2)]);
                else
                    result += string(1, s[location + (i/2) * (numRows + numRows - 2)+2*numRows-4-2*(location-1)]);
            }   
            ++location;
        }
        return result;
    }
};
```
