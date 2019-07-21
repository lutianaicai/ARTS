# 第19周

## Algorithm

### LeetCode 844. 比较含退格的字符串

给定 S 和 T 两个字符串，当它们分别被输入到空白的文本编辑器后，判断二者是否相等，并返回结果。 # 代表退格字符。


示例 1：

```
输入：S = "ab#c", T = "ad#c"
输出：true
解释：S 和 T 都会变成 “ac”。
```

示例 2：

```
输入：S = "ab##", T = "c#d#"
输出：true
解释：S 和 T 都会变成 “”。
```

示例 3：

```
输入：S = "a##c", T = "#a#c"
输出：true
解释：S 和 T 都会变成 “c”。
```

示例 4：

```
输入：S = "a#c", T = "b"
输出：false
解释：S 会变成 “c”，但 T 仍然是 “b”。
```

#### Solution : 

耗时: 0 ms
内存: 8.4 MB

```cpp
class Solution {
public:
  bool backspaceCompare(string S, string T) {
    stack<char> s;
    stack<char> t;
    for (int i=0; i<S.length(); i++) {
      if (S[i] == '#') {
        if (!s.empty()) {
          s.pop();
        }
      } else {
        s.push(S[i]);
      }
    }
    for (int i=0; i<T.length(); i++) {
      if (T[i] == '#') {
        if (!t.empty()) {
          t.pop();
        }
      } else {
        t.push(T[i]);
      }
    }
    if (s.size() != t.size()) {
      return false;
    }
    while (s.size() != 0) {
      if (s.top() == t.top()) {
        s.pop();
        t.pop();
      } else {
        return false;
      }
    }
    return true;
  }
};

```


## Review

[Generalizing Swift code](https://www.swiftbysundell.com/posts/generalizing-swift-code) 作者介绍了一些抽象 Swift 代码的心得与技巧。

## Tip

Swift 5.1 中枚举可以指定默认值了

```swift
// Associated enum value defaults are specified the same way as
// default function arguments:
enum Content {
    case text(String)
    case image(Image, description: String? = nil)
    case video(Video, autoplay: Bool = false)
}

// At the call site, any associated value that has a default
// can be omitted, and the default will be used:
let video = Content.video(Video(url: url))
```

## Share

本周分享 [谈谈 MVX 中的 Model](https://draveness.me/mvx-model) 灯塔对于 MVX 的理解。

