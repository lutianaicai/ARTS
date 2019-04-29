# 第7周

## Algorithm

### LeetCode 120. 三角形最小路径和

给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。

例如，给定三角形：

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。

#### Solution 1 二维数组

耗时: 12ms
内存: 10.1MB

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int> > &triangle) 
    {
        vector<vector<int> > mini(triangle.size()+1, vector<int>(triangle.size()+1, 0));
        for (int i = triangle.size() - 1; i >= 0; i--)
        {   
            vector<int> curTr = triangle[i];
            for (int j = 0; j < curTr.size(); j++)
            {
                mini[i][j] = min(mini[i+1][j], mini[i+1][j+1]) + curTr[j];
            }
        }
        return mini[0][0];
    }
};
```

#### Solution 2 一维数组

耗时: 12ms
内存: 9.8MB

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int> > &triangle) 
    {
        vector<vector<int> > mini(triangle.size()+1, vector<int>(triangle.size()+1, 0));
        for (int i = triangle.size() - 1; i >= 0; i--)
        {   
            vector<int> curTr = triangle[i];
            for (int j = 0; j < curTr.size(); j++)
            {
                mini[i][j] = min(mini[i+1][j], mini[i+1][j+1]) + curTr[j];
            }
        }
        return mini[0][0];
    }
};
```


## Review

[Structuring model data in Swift](https://www.swiftbysundell.com/posts/structuring-model-data-in-swift)
作者对设计model结构进行了讨论，提出了四点建议：
1. model要具有清晰层级关系
2. 避免副本的产生
3. 为一些业务的集中处理，可以使用递归结构
4. 对于一些可以复用之前结构model的业务，在特殊情况下，也要敢于特例化model

model结构的设计其实跟实际业务的关联是分不开的，需要在复用以及避免复杂设计中间找平衡。

## Tip

iOS 中，`IOKit framework` 是专门用于跟硬件或内核服务通讯的。可以使用 `IOKit framework` 获取电量消耗信息。

## Share

本周分享 [微信iOS卡顿监控系统](https://mp.weixin.qq.com/s?__biz=MzAwNDY1ODY2OQ==&mid=207890859&idx=1&sn=e98dd604cdb854e7a5808d2072c29162&scene=4) 微信卡顿监控系统思路分析。原理以及细节都很有深度，值得多看。


