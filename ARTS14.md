# 第14周

## Algorithm

### LeetCode 322. 零钱兑换

给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。


示例 1：

```
输入: coins = [1, 2, 5], amount = 11
输出: 3 
解释: 11 = 5 + 5 + 1

```

示例 2：

```
输入: coins = [2], amount = 3
输出: -1

```



#### Solution 	

耗时: 132 ms
内存: 12.6 MB

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int Max = amount + 1;
        vector<int> dp(amount + 1, Max);
        dp[0] = 0;
        for (int i = 0; i <= amount; i++)
        {
            for (int j = 0; j < coins.size(); j++)
            {
                if (coins[j] <= i)
                {
                    dp[i] = min(dp[i], dp[i - coins[j]] + 1);
                }      
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
    }
};
```


## Review

[The Swift 5.1 features that power SwiftUI’s APIt](https://www.swiftbysundell.com/posts/the-swift-51-features-that-power-swiftuis-api)
作者简单介绍了SwiftUI中引入了的Swift5.1新特性。诸如：Opaque return types，Omitted return keywords，Function builders。

## Tip

`Xcode`中`shift+command+L`快捷键可以迅速打开控件库相信很多人都知道，但是拖一个控件后，控件库就消失就很烦。其实`shift+option+command+L`可以把控件库固定在屏幕上。

## Share

本周分享 [Immutable models and data consistency in our iOS App](https://medium.com/@Pinterest_Engineering/immutable-models-and-data-consistency-in-our-ios-app-d10e248bfef8)作者是 Pinterest的iOS团队，文章有一些些老，关注大牛当时的设计思想即可。


