# 第17周

## Algorithm

### LeetCode 231. 2的幂

给定一个整数，编写一个函数来判断它是否是 2 的幂次方。


示例 1：

```
输入: 1
输出: true
解释: 20 = 1

```

示例 2：

```
输入: 16
输出: true
解释: 24 = 16

```

示例 3：

```
输入: 218
输出: false

```



#### Solution 1 : 

耗时: 4 ms
内存: 8.1 MB

```cpp
class Solution {
public:
    bool isPowerOfTwo(int n) {
        if(n==1) return true;
        long mi=2;//防止溢出所以用long类型
        while(mi<=n)
        {
            if(mi==n)
                return true;
            else
            {
                mi*=2;
                if(mi>INT_MAX)
                    break;
            }
        }
        return false;
    }
};

```

#### Solution 2 : 

耗时: 0 ms
内存: 8 MB

```cpp
class Solution {
public:
    bool isPowerOfTwo(int n) {
        if(n<=0) return false;
        if((n&n-1)==0) return true;
        return false;
    }
};

```


## Review

[Configurable types in Swift](https://www.swiftbysundell.com/posts/configurable-types-in-swift)作者介绍了 Swift 中，如何协议、扩展、工厂模式等方式进行可配置类型对象初始化工作。

## Tip

`Xcode` 中 `preview` 功能可以实现 storyboard 中界面在多机型界面查看 UI 适配情况。

## Share

本周分享 [如何优雅地使用 KVO](https://draveness.me/kvocontroller) 灯塔对 KVOController 的原理解读。

