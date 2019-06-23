# 第15周

## Algorithm

### LeetCode 152. 乘积最大子序列

给定一个整数数组 nums ，找出一个序列中乘积最大的连续子序列（该序列至少包含一个数）。


示例 1：

```
输入: [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。

```

示例 2：

```
输入: [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。

```



#### Solution 	

耗时: 12 ms
内存: 9.1 MB

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        if (nums.empty()) return 0;

        int max[nums.size()];
        int min[nums.size()];

        max[0] = min[0] = nums[0];
        int res = nums[0];
        for (int i = 1; i < nums.size(); i++)
        {
            if (nums[i] > 0)
            {   
                max[i] = max[i-1] > 0 ? max[i-1] * nums[i]:nums[i];
                min[i] = min[i-1] < 0 ? min[i-1] * nums[i]:nums[i];
            }
            else 
            {
                max[i] = min[i-1] < 0 ? min[i-1] * nums[i]: nums[i];
                min[i] = max[i-1] > 0 ? max[i-1] * nums[i]: nums[i];
            }
            res = res > max[i] ? res: max[i];
        }
        return res;
    }
};
```


## Review

[Using the factory pattern to avoid shared state in Swift](https://www.swiftbysundell.com/posts/using-the-factory-pattern-to-avoid-shared-state-in-swift?rq=factories) 作者简单介绍了 Swift 中，利用工厂方法代替单例以避免单例状态混乱引起的麻烦。

## Tip

`Xcode` 中 `shift+左键` 可以实现多重光标，可以一次给多个方法添加类似 privae 属性。

## Share

本周分享 [Optimizing Images](https://www.swiftjectivec.com/optimizing-images/) 作者分享了一些 UIKit 处理图片的底层机制。


