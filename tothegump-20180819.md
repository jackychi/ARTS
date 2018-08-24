## leetcode 算法题
> https://leetcode.com/problems/maximum-product-of-word-lengths/description/

```Python
class Solution:
    def maxProduct(self, words):
        """
        :type words: List[str]
        :rtype: int
        """
        cache = {}
        for word in words:
            bitnum = 0
            for c in set(word):
                bitnum |= 1 << (ord(c) - 97)
            cache[bitnum] = max(cache.get(bitnum, 0), len(word))
        return max([cache[x] * cache[y] for x in cache for y in cache if not x & y] or [0])
```

## 英文技术文章地址和简要点评
> https://content.pivotal.io/blog/understanding-when-to-use-rabbitmq-or-apache-kafka

非常清晰的说明了两者的特点及适用场景，但发现还需要更明确的示例来说明，给自己挖个坑，后面填上
## 学习了什么新的技术技巧
最近在学习并实践基于 gitlab 的 CI/CD
## 分享一篇有观点和思考的技术文章，长短都可
> http://blog.tothegump.com/2018/06/18/dtp-1/
这是自己写的关于分布式事务的文章，就推荐这个吧
