# 第18周

## Algorithm

### LeetCode 19. 删除链表的倒数第N个节点

给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。


示例 ：

```
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.

```

#### Solution 1 : 

耗时: 8 ms
内存: 8.5 MB

```cpp
class Solution {
public:
  ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    ListNode* first = dummy;
    ListNode* second = dummy;
    for (int i=0; i<n; i++) {
      if (first->next == nullptr) {
        return head;
      }
      first = first->next;
    }
    while (first->next != nullptr) {
      first = first->next;
      second = second->next;
    }
    second->next = second->next->next;
    return dummy->next;
  }
};

```

#### Solution 2 : 

耗时: 4 ms
内存: 8.4 MB

```cpp
class Solution {
public:
  ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    ListNode* first = dummy;
    ListNode* second = dummy;
    for (int i=0; i<=n; i++) {
      first = first->next;
    }
    while (first != nullptr) {
      first = first->next;
      second = second->next;
    }
    second->next = second->next->next;
    return dummy->next;
  }
};

```


## Review

[Customizing Codable types in Swift](https://www.swiftbysundell.com/posts/customizing-codable-types-in-swift)作者介绍了 Swift 中，struct 与 json 的一些转码的高级技巧。

## Tip

`Xcode` 中 `#warning()` 可以加入不影响编译的警告，警告要比 TODO 注释更加清晰，在工期紧时候添加还不影响编译。以后有时间了再重构。 

## Share

本周分享 [关于离屏渲染的深入研究](https://medium.com/@jasonyuh/%E5%85%B3%E4%BA%8E%E7%A6%BB%E5%B1%8F%E6%B8%B2%E6%9F%93%E7%9A%84%E6%B7%B1%E5%85%A5%E7%A0%94%E7%A9%B6-e776f56b3e60) 即刻 iOS leader Jason Yu 对离屏渲染方面的研究。

