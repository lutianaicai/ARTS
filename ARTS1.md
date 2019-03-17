# 第1周

## Algorithm

### LeetCode 98. 验证二叉搜索树

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

节点的左子树只包含小于当前节点的数。
节点的右子树只包含大于当前节点的数。
所有左子树和右子树自身必须也是二叉搜索树。

#### Solution 1

耗时: 56ms
内存: 16.3MB


```
class Solution(object):
    def isValidBST(self, root):
        inorder = self.inorder(root)
        return inorder == list(sorted(set(inorder)))
        
    def inorder(self, root):
        if root is None:
            return []
        return self.inorder(root.left) + [root.val] + self.inorder(root.right)
```

耗时: 48ms
内存: 15.9MB


```
class Solution(object):
    def isValidBST(self, root):
        self.prev = None
        return self.helper(root)
        
    def helper(self, root):
        if root is None:
            return True
        if not self.helper(root.left):
            return False
        if self.prev and self.prev.val >= root.val:
            return False
        self.prev = root
        return self.helper(root.right)
```



## Review

[The power of UserDefaults in Swift](https://www.swiftbysundell.com/posts/the-power-of-userdefaults-in-swift) 
众所周知UserDefaults可以作为用户偏好设置的持久化方案。本文介绍了除此以外的其他用法。
* 可以为组间App提供共享数据
* 在App加载时重写一些数值
* 自由进行单元测试

UserDefaults虽然不能直接当作数据库使用，但是其实还是能为我们写单元测试以及debug作出很多贡献。

## Tip

Swift中实现synchronized

Objective-C中`@synchronized`关键字可以实现代码块加锁的操作。Swift中没有提供对应关键字，需要自己实现。

以下是`RxSwift`实现方式:

```
extension Reactive where Base: AnyObject {
    func synchronized<T>(_ action: () -> T) -> T {
        objc_sync_enter(self.base)
        let result = action()
        objc_sync_exit(self.base)
        return result
    }
}
```

可以看出是基于`objc_sync_enter`和`objc_sync_exit`来实现。OC中也是基于这两个函数实现的。[源代码](https://github.com/gcc-mirror/gcc/blob/master/libobjc/objc/objc-sync.h)

本Tip来自[知识小集](https://github.com/awesome-tips/iOS-Tips/blob/master/2019/01.md)，作者[南峰子](https://www.weibo.com/touristdiary?is_hot=1)

## Share

本周分享[深入理解RunLoop](https://blog.ibireme.com/2015/05/18/runloop/) ibireme大神雄文，从源码级别探究RunLoop概念以及底层实现原理。

