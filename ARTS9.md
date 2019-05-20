# 第9周

## Algorithm

### LeetCode 300. 最长上升子序列

给定一个无序的整数数组，找到其中最长上升子序列的长度。

示例 ：

```
输入: [10,9,2,5,3,7,101,18]
输出: 4 
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
```


#### Solution 1 DP

耗时: 64ms
内存: 8.6MB

```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        if (&nums == nullptr || nums.size() == 0)
        {
            return 0;
        }
    
        int res = 1;
        vector<int> dp(nums.size() + 1);

        for (int i = 0; i < nums.size(); i++) dp[i] = 1;

        for (int i = 1; i < nums.size(); i++)
        {
            for (int j = 0; j < i; j++)
            {
                if (nums[j] < nums[i])
                {
                    dp[i] = max(dp[i], dp[j] + 1);
                }
            }
            res = max(res, dp[i]);
        }
        return res;
    }
};
```
#### Solution 2 二分剪枝

耗时: 12ms
内存: 8.8MB

```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        vector<int> res;
        for (int i = 0; i < nums.size(); i++)
        {
            auto it = std::lower_bound(res.begin(), res.end(), nums[i]);
            if (it == res.end())
                res.push_back(nums[i]);
            else *it = nums[i];
        }
        return res.size();
    }
};
```

## Review

[Pure functions in Swift](https://www.swiftbysundell.com/posts/pure-functions-in-swift)
作者认为好的函数，应该是不带来任何副作用，不依赖任何外部状态，对于指定入参永远给出相同输出，而且易于测试。

## Tip

iOS 中，[SkyLab](https://github.com/mattt/SkyLab) 是著名的`A/Btest` SDK可以通过 `NSUserDefault` 保存策略，使每个测试桶中的用户保持相同策略。

## Share

本周分享 [GYDataCenter：高性能数据库框架](https://wereadteam.github.io/2016/07/06/GYDataCenter/) 微信团队设计`GYDataCenter`的思路。


