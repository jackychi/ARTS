
# 1.Algorithm
> 每周至少做一个 leetcode 的算法题

随机到一个 easy，刚好本周时间不多

https://leetcode.com/problems/valid-parentheses/


> Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
> An input string is valid if:
> Open brackets must be closed by the same type of brackets.
> Open brackets must be closed in the correct order.
> Note that an empty string is also considered valid.


```
class Solution:
    pairs = [('(', ')'), ('[', ']'), ('{', '}')]
    
    def is_valid(self, s: str) -> bool:
        l = []
        left = [l for l, _ in self.pairs]
        right = [r for _, r in self.pairs]
        for i in s:
            if i in left:
                l.append(i)
            elif i in right:
                if len(l) > 0 and s# elf.is_pair(l[-1], i):
                    l.pop()
                else:
                    return False
        if len(l) > 0:
            return False
        return True

    def is_pair(self, a, b):
        return (a, b) in self.pairs
```
 基本思路就是入栈出栈，需要注意就是最后要判断栈为空

# 2.Review
> 阅读并点评至少一篇英文技术文章

https://github.com/spring-projects/spring-boot/blob/master/README.adoc

其实 Spring Boot 的文档看了好几个，这里挑有代表性的一篇
整体来说，主要是讲 Spring Boot 项目本身的内容（而不是使用），如何构建，以及 Spring Boot 项目本身团队协作的一些基本要求。

# 3.Tip
> 学习至少一个技术技巧

 - Java 刚看完了《深入理解 Java 虚拟机》(虽然这个持续了好多周，刚好这是最后一周)

- Geektime 的专栏也看了一点，不过没有记录，之后会有详细记录

# 4.Share
> 分享一篇有观点和思考的技术文章
本周输出：
http://blog.tothegump.com/chinwag/java_learning.html
主要是最近学习 Java 的一些大致感受。
