# 第1周

## Algorithm

### LeetCode 236. 二叉树的最近公共祖先

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

#### Solution 

耗时: 88ms
内存: 23.5MB


```
class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        if not root or root == q or root == p:
            return root
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        if not left:
            return right
        if not right:
            return left
        return root
```



## Review

[Avoiding race conditions in Swift](https://www.swiftbysundell.com/posts/avoiding-race-conditions-in-swift)
文章给出了一个竞态条件可能会引发逻辑问题的案例。并且由浅入深，给出了单线程解决方案（handler array）和保证线程安全的多线程解决方案（GCD）

结尾作者也发表了自己的思考，他认为完全避免竞态资源是不可能的。但是目前的技术手段确实可以很大程度的确保代码可以按逻辑执行。而且他个人认为与其所有的代码都保证线程安全不如在设计API时牢记在心。毕竟大部分代码运行在主线程，全部保证安全有过度设计之嫌。

## Tip

使用终端命令时如果出现`Command Not Found`错误绝大多数时由于用户 `$PATH`设置不正确

首先echo $PATH查看环境变量是否已存在可执行文件的路径，如果没有就打开`.bash_profile`把可执行文件的绝对路径写进去

```
➜ vi $HOME/.bash_profile
export PATH="$HOME/Library/Android/flutter/bin:$PATH"

// 想让刚配置的 PATH 生效，需要刷新终端
➜  source $HOME/.bash_profile
```

本Tip来自[知识小集](https://github.com/awesome-tips/iOS-Tips/blob/master/2019/01.md)，作者[Lefe_x](https://www.weibo.com/u/5953150140)

## Share

本周分享[再看关于 Storyboard 的一些争论](https://onevcat.com/2017/04/storyboard-argue/) 喵神对Storyboard使用的一些思考和实践经验分享。虽然是17年的文章，但是还是能带来很多思考。

