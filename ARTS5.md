# 第5周

## Algorithm

### LeetCode 69. x 的平方根

实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去

#### Solution 1 二分法

耗时: 44ms
内存: 11.6MB

```
class Solution(object):
    def mySqrt(self, x):
        if x == 1 or x == 0:
            return x
        left,right,res = 0,x,0
        while left <= right:
            mid = int(left + (right - left)/2)
            if mid > x/mid:
                right = mid - 1
            elif mid < x/mid:
                left = mid + 1
                res = mid
            else:
                return int(mid)
        return int(res)
```

#### Solution 2 牛顿迭代法

耗时: 48ms
内存: 11.7MB

```
class Solution(object):
    def mySqrt(self, x):
        if x <= 1:
            return x
        r = x
        while r > x / r:
            r = (r + x / r) / 2
        return int(r)
```


## Review

[Reflection in Swift](https://www.swiftbysundell.com/posts/reflection-in-swift)
作者利用改造UserSession为例，介绍了如何利用Protocol Mirror进行运行时动态递归调用Reset方法，提高代码的鲁棒性。

同时还给出了目前Mirror的局限，例如目前只能读取属性还不能动态写入。

作者认为反射机制确实功能强大，但是在日常开发时候引入需要先思考是否必要，也许代码的可读性和易维护行更加重要。

## Tip

iOS 开发过程中可以通过[Injection](https://itunes.apple.com/cn/app/injectioniii/id1380446739?l=en&mt=12)进行 App 动态调试，不需重新编译，大幅提高 debug 效率。

安装后选择项目，在项目`didFinishLaunchingWithOptions`方法中加入:

```
Xcode 10.2 and later:

#if DEBUG
Bundle(path: "/Applications/InjectionIII.app/Contents/Resources/iOSInjection.bundle")?.load()
//for tvOS:
Bundle(path: "/Applications/InjectionIII.app/Contents/Resources/tvOSInjection.bundle")?.load()
//Or for macOS:
Bundle(path: "/Applications/InjectionIII.app/Contents/Resources/macOSInjection.bundle")?.load()
#endif
```


## Share

本周分享[GYHttpMock：iOS HTTP请求模拟工具](http://wereadteam.github.io/2016/02/25/GYHttpMock/)微信读书团队的一篇关于模拟`Http`请求的文章。其实现原理核心包括`request`匹配、`request`拦截、`response`替换三个部分。


