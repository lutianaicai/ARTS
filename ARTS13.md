# 第13周

## Algorithm

### LeetCode 146. LRU缓存机制

运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果密钥 (key) 存在于缓存中，则获取密钥的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果密钥不存在，则写入其数据值。当缓存容量达到上限时，它应该在写入新数据之前删除最近最少使用的数据值，从而为新的数据值留出空间。

进阶：

```
你是否可以在 O(1) 时间复杂度内完成这两种操作？
```

示例 1：

```
LRUCache cache = new LRUCache( 2 /* 缓存容量 */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // 返回  1
cache.put(3, 3);    // 该操作会使得密钥 2 作废
cache.get(2);       // 返回 -1 (未找到)
cache.put(4, 4);    // 该操作会使得密钥 1 作废
cache.get(1);       // 返回 -1 (未找到)
cache.get(3);       // 返回  3
cache.get(4);       // 返回  4

```



#### Solution 	

耗时: 136 ms
内存: 38.2 MB

```cpp
class LRUCache
{
private:
	struct LRUCacheNode
	{
		int key;
		int value;
	};

public:
	LRUCache(int cap)
	{
		capacity = cap;
	}

	void put(const int& key, const int& v)
	{
		auto findIter = cacheHolder.find(key);
		if (cacheHolder.end() != findIter) //如果能找到key值，更新即可
		{
			keyElement.splice(keyElement.begin(), keyElement, findIter->second);
			findIter->second->value = v;
		}

		else
		{
			LRUCache::LRUCacheNode node;
			node.key = key;
			node.value = v;
			keyElement.push_front(node);

			cacheHolder[key] = keyElement.begin();

			if (cacheHolder.size() > capacity) //如果容量超限了，删除list的back
			{
				cacheHolder.erase(keyElement.back().key);
				keyElement.pop_back();
			}
		}
		
	}

	int get(const int& key)
	{
		auto findIter = cacheHolder.find(key);
		if (cacheHolder.end() != findIter)
		{
			int value = (findIter->second)->value;

			keyElement.splice(keyElement.begin(), keyElement, findIter->second); //[1,3,4,5](iterator==4) --> (4,1,3,5)
			return value;
		}

		return -1;
	}

private:
	list<LRUCache::LRUCacheNode>								keyElement;		//存储的key值
	unordered_map<int, list<LRUCache::LRUCacheNode>::iterator >	cacheHolder;	//实际上存储的数据
	int															capacity;		//cache的容量
};
```


## Review

[Dependency injection using factories in Swift](https://www.swiftbysundell.com/posts/dependency-injection-using-factories-in-swift)
作者介绍了Swift中利用工厂方式来对对象进行依赖注入的方式，代替全局变量，不实用单例，使得但愿测试更加容易。

## Tip

`Xcode`中代码行数左边会有一条蓝条代表你这段代码还没有`commit`，但是有时候我们有时候会忘记修改了什么，或是想改回去，只需要右键这段蓝条`discard change`就可以了

## Share

本周分享 [Re-architecting Pinterest’s iOS app](https://medium.com/@Pinterest_Engineering/re-architecting-pinterest-039-s-ios-app-e0a2d34a6ac2)作者是 Pinterest的iOS团队，虽说是16年重构代码时的想法，但是现在看来一些重要的点从不过时。


