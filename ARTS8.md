# 第8周

## Algorithm

### LeetCode 123. 买卖股票的最佳时机 III

给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 两笔 交易。

注意: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

示例 1：

```
输入: [3,3,5,0,0,3,1,4]
输出: 6
解释: 在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。
     随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。
```


#### Solution DP

耗时: 12ms
内存: 9.5MB

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int hold1 = INT_MIN, hold2 = INT_MIN;
        int release1 = 0, release2 = 0;
        for (int i : prices)
        {
            release2 = max(release2, hold2+i);
            hold2    = max(hold2,    release1-i);
            release1 = max(release1, hold1+i);
            hold1    = max(hold1,    -i);
        }
        return release2;
    }
};
```


## Review

[Property observers in Swift](https://www.swiftbysundell.com/posts/property-observers-in-swift)
作者对`swift`中的属性观察进行了详细的介绍。例如可以利用`willSet` `didSet`进行属性的自动更新，`view`的参数设置，参数输入校验等功能。完全无需其他框架的引入。

## Tip

iOS 中，[Lottie](http://airbnb.io/lottie/#/) 可以实现直接加载渲染AE动画导出的json文件，生成炫酷动画的功能。

## Share

本周分享 [深入剖析 WebKit](https://ming1016.github.io/2017/10/11/deeply-analyse-webkit/) 戴铭大神对`WebKit`的详细分析。


