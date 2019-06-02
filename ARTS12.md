# 第12周

## Algorithm

### LeetCode 547. 朋友圈

班上有 N 名学生。其中有些人是朋友，有些则不是。他们的友谊具有是传递性。如果已知 A 是 B 的朋友，B 是 C 的朋友，那么我们可以认为 A 也是 C 的朋友。所谓的朋友圈，是指所有朋友的集合。

给定一个 N * N 的矩阵 M，表示班级中学生之间的朋友关系。如果M[i][j] = 1，表示已知第 i 个和 j 个学生互为朋友关系，否则为不知道。你必须输出所有学生中的已知的朋友圈总数。

示例 1：

```
输入: 
[[1,1,0],
 [1,1,0],
 [0,0,1]]
输出: 2 
说明：已知学生0和学生1互为朋友，他们在一个朋友圈。
第2个学生自己在一个朋友圈。所以返回2。
```

示例 2：

```
输入: 
[[1,1,0],
 [1,1,1],
 [0,1,1]]
输出: 1
说明：已知学生0和学生1互为朋友，学生1和学生2互为朋友，所以学生0和学生2也是朋友，所以他们三个在一个朋友圈，返回1。
```



#### Solution : Union find	

耗时: 40ms
内存: 10.9MB

```cpp
class Solution {
public:
    vector<int> *fr = nullptr;
    int findparent(int m) {
        while ((*fr)[m]>=0) m = (*fr)[m];
        return m;
    }

    bool befriend(int x, int y) {
        if (findparent(x) != findparent(y)) return false;
        else return true;
    }

    void unioning(int x, int y) {
        x = findparent(x);
        y = findparent(y);
        if ((*fr)[x] < (*fr)[y]) {
            (*fr)[x] += (*fr)[y];
            (*fr)[y] = x;
        }
        else {
            (*fr)[y] += (*fr)[x];
            (*fr)[x] = y;
        }
    }

    int findCircleNum(vector<vector<int> >& M) {
        int m = M.size(), n = M.size();
        vector<int> fr_(n, -1);
        fr = &fr_;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (M[i][j] == 1 && !befriend(i, j)) {
                    unioning(i, j);
                    m--;
                }
            }
        }
        return m;
    }
};
```


## Review

[Avoiding singletons in Swift](https://www.swiftbysundell.com/posts/avoiding-singletons-in-swift)
作者介绍了Swift中单例的三种缺陷：
1.他们是全局可修改的状态
2.依赖单例的代码不易管控
3.管理单例的生命周期十分吊诡

所以引入依赖注入的方式解决对单例的依赖。

## Tip

`Xcode`中如果有方法不知道取什么名字，但是你知道你以后要来写这个方法，可以用`<#name#>`方式保留一个命名空间，并不会打断代码。

## Share

本周分享 [如何打造易扩展的高性能图片组件](https://zhuanlan.zhihu.com/p/26955368?utm_medium=social&utm_source=weibo2)作者从架构设计，核心性能优化两方面，分享如何开发这样一个易扩展的高性能图片组件。


