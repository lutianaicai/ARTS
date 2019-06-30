# 第16周

## Algorithm

### LeetCode 191. 位1的个数

编写一个函数，输入是一个无符号整数，返回其二进制表达式中数字位数为 ‘1’ 的个数（也被称为汉明重量）。


示例 1：

```
输入：00000000000000000000000000001011
输出：3
解释：输入的二进制串 00000000000000000000000000001011 中，共有三位为 '1'。

```

示例 2：

```
输入：00000000000000000000000010000000
输出：1
解释：输入的二进制串 00000000000000000000000010000000 中，共有一位为 '1'。

```

示例 3：

```
输入：11111111111111111111111111111101
输出：31
解释：输入的二进制串 11111111111111111111111111111101 中，共有 31 位为 '1'。

```



#### Solution 1 : 与操作

耗时: 4 ms
内存: 8.2 MB

```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int res=0;
        while(n)
        {
            res+=n&1;
            n>>=1;
        }
        return res;
    }
};
```

#### Solution 2 : 取余法

耗时: 12 ms
内存: 8.2 MB

```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int res=0;
        while(n)
        {
            res+=n%2;
            n>>=1;
        }
        return res;
    }
};

```

#### Solution 3 : 去掉尾部的 1

耗时: 8 ms
内存: 8.1 MB

```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int ans=0;
        while(n)
        {
            ans++;
            n&=n-1;
        }
        return ans;
    }
};

```


## Review

[Shifting paradigms in Swift](https://www.swiftbysundell.com/posts/shifting-paradigms-in-swift) 作者介绍了 Swift 中，如何利用工厂模式兼容 SwiftUI。简单来讲就是写两遍（玩笑）。

## Tip

`Xcode` 中 `option+左键框选` 可以实现类似修改一些 `let` 属性到 `var` 属性。

## Share

本周分享 [Cleaner Classes with Structs and Tuples](https://appventure.me/posts/2019-02-24-anonymous-tuple-structs.html) 作者分享了一些 Swift 中对复杂类通过 struct 和 tuple 进行结构化的技巧。


