# 第3周

## Algorithm

### LeetCode 102. 二叉树的层次遍历

给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。

#### Solution 1 BFS

耗时: 40ms
内存: 12.2MB

```
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root: return []
        
        result = []
        queue = collections.deque()
        queue.append(root)
        
        while queue:
            level_size = len(queue)
            current_level = []
            
            for _ in range(level_size):
                node = queue.popleft()
                current_level.append(node.val)
                if node.left: queue.append(node.left)
                if node.right: queue.append(node.right)
                
            result.append(current_level)
        
        return result
```

#### Solution 2 DFS

耗时: 56ms
内存: 12.4MB

```
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root: return []
        self.result = []
        self._dfs(root, 0)
        return self.result
    
    def _dfs(self, node, level):
        if not node: return 
        
        if len(self.result) < level + 1:
            self.result.append([])
            
        self.result[level].append(node.val)
        
        self._dfs(node.left, level + 1)
        self._dfs(node.right, level + 1)
```


## Review

[Different flavors of type erasure in Swift](https://www.swiftbysundell.com/posts/different-flavors-of-type-erasure-in-swift)
文章给出了利用类型擦除解决实际问题的案例。给出了范型、闭包等方案

作者认为Swift严格的类型检查解除了产生了很多未知bug的隐患，但有时候利用类型擦除隐藏类的一些特性只关注类型本身还是会给开发带来很多好处。

## Tip

自己写的项目更新Xcode10.2后报错`Module compiled with Swift 5 cannot be imported in Swift 4.2`

原因应该是Carthage是用Swift4.2编译的，升级之后不兼容，解决办法：

```
rm -rf ~/Library/Caches/org.carthage.CarthageKit/DerivedData
carthage update --no-use-binaries --platform iOS
```


## Share

本周分享[iOS 组件化方案探索](http://wereadteam.github.io/2016/03/19/iOS-Component/) bang神在微信读书团队的一篇关于组件化探索的文章。目前而言，我还没有相关经验。主要负责项目还太小，继续探索中。


