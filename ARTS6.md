# 第6周

## Algorithm

### LeetCode 70. 爬楼梯

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数

#### Solution 1 记忆化递归

耗时: 8ms
内存: 8.3MB

```cpp
class Solution {
public:
    int climbStairs(int n) {
        vector<int> memo(n+1, 0);
        return helper(0, n, memo);
    }
    
    int helper(int i, int n, vector<int> &memo) {
        if (i > n)
        {
            return 0;
        }
        if (i == n)
        {
            return 1;
        }
        if (memo[i] > 0)
        {
            return memo[i];
        }
        memo[i] = helper(i+1, n, memo) + helper(i+2, n, memo);
        return memo[i];
    }
};
```

#### Solution 2 动态规划

耗时: 8ms
内存: 8.5MB

```cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n == 1) {
            return 1;
        }
        vector<int> dp(n+1, 0);
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; ++i) {
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
};
```

#### Solution 3 斐波那契数

耗时: 4ms
内存: 8.1MB

```cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n == 1) {
            return 1;
        }
        int first = 1;
        int second = 2;
        for (int i = 3; i <= n; ++i) {
            int third = first + second;
            first = second;
            second = third;
        }
        return second;
    }
};
```


## Review

[Designing Swift APIs](https://www.swiftbysundell.com/posts/designing-swift-apis)
作者对API设计进行了讨论，提出了五点建议：
1. 函数名的调用要有自解性
2. 内嵌类型进行`extension`封装
3. 具有强的类型匹配(比如`struct`代替简单的`String`匹配)
4. 可伸缩的APIs，可以让调用者只关心关键参数
5. 进行便利封装

## Tip

iOS 开发过程中可以通过[LSUnusedResources](https://github.com/tinymind/LSUnusedResources)找出项目中的无用图片，减少包大小。


## Share

本周分享[预加载与智能预加载（iOS）](https://draveness.me/preload.html)灯塔关于TableView网络请求主流预加载的分析。


