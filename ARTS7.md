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


