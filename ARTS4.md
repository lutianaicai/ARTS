# 第4周

## Algorithm

### LeetCode 22. 括号生成

给出 n 代表生成括号的对数，请你写出一个函数，使其能够生成所有可能的并且有效的括号组合。

#### Solution 

耗时: 36ms
内存: 12.1MB

```
class Solution(object):
    def generateParenthesis(self, n):
        self.list = []
        self._gen(0, 0, n, "")
        return self.list
    
    def _gen(self, left, right, n, result):
        if left == n and right == n:
            self.list.append(result)
            return
        if left < n:
            self._gen(left + 1, right, n, result + "(")
        if left > right and right < n:
            self._gen(left, right + 1, n, result + ")")
```


## Review

[Bindable values in Swift](https://www.swiftbysundell.com/posts/bindable-values-in-swift)
作者给出了一种UI绑定Model values的演示，很像Rxswift Bind的用法。

作者认为这种UI绑定values的写法可以避免很多诸如observation closure带来的循环引用，数据实时更新带来的多重网络请求等问题。

## Tip

开发过程中可以在运行时动态加载`Framework/Library`。方法是使用`dlfcn.h`的`dlopen`函数:

```
void *framework1Handle = dlopen("DynamicFramework1.framework/DynamicFramework1", RTLD_LAZY);
```

本Tip来自[知识小集](https://github.com/awesome-tips/iOS-Tips/blob/master/2018/01.md)，作者[南峰子](https://www.weibo.com/touristdiary?is_hot=1)


## Share

本周分享[iOS 启动连续闪退保护方案](http://wereadteam.github.io/2016/05/23/GYBootingProtection/)微信读书团队的一篇关于iOS 启动连续闪退保护方案的文章。探讨了连续闪退问题的产生原因、检测、修复机制。


