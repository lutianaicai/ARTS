# 第10周

## Algorithm

### LeetCode 300. 编辑距离

给定两个单词 word1 和 word2，计算出将 word1 转换成 word2 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

1. 插入一个字符
2. 删除一个字符
3. 替换一个字符

示例 1：

```
输入: word1 = "horse", word2 = "ros"
输出: 3
解释: 
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
```

示例 2：

```
输入: word1 = "intention", word2 = "execution"
输出: 5
解释: 
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')
```


#### Solution 

耗时: 16ms
内存: 11.2MB

```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int m = word1.length();
        int n = word2.length();

        vector<vector<int> > dp(m+1, vector<int>(n+1));

        for (int i = 0; i <= m; i++) {
            dp[i][0] = i;
        }
        for (int j = 0; j <= n; j++) {
            dp[0][j] = j;
        }
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1[i-1] == word2[j-1]) {
                    dp[i][j] = dp[i-1][j-1];
                } else {
                    dp[i][j] = 1 + min(dp[i-1][j-1], min(dp[i][j-1], dp[i-1][j]));
                }
            }
        }
        return dp[m][n];
    }
};
```


## Review

[Wrapping sequences in Swift](https://www.swiftbysundell.com/posts/wrapping-sequences-in-swift)
作者利用swift中的Sequence进行再封装的案例。展示了基于sequence我们可以把复杂的逻辑隐藏在简洁的API背后。

## Tip

iOS 中，涉及浮点数展示，计算建议直接使用 [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber) 因为精度实在是太容易出问题了。

## Share

本周分享 [使用 ASDK 性能调优 - 提升 iOS 界面的渲染性能](https://draveness.me/asdk-rendering) 灯塔的渲染性能分析文章，从视图渲染层面讲解 ASDK 对渲染过程的优化。


