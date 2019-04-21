# 2019-04-21
**# 1.Algorithm**
> 每周至少做一个 leetcode 的算法题  
https://leetcode.com/problems/number-of-longest-increasing-subsequence/

```Python
class Solution:
    def findNumberOfLIS(self, nums: List[int]) -> int:
        l = len(nums)
        dp = [1] * l
        count = [1] * l
        max_len = 1
        for i in range(1, l):
            for j in range(i):
                if nums[j] < nums[i] and dp[j] +1 > dp[i]:
                    dp[i] = dp[j] + 1
                    count[i] = count[j]
                elif nums[j] < nums[i] and dp[j] + 1 == dp[i]:
                    count[i] += count[j]
            max_len = max(max_len, dp[i])
        res = 0
        for k in range(l):
            if dp[k] == max_len:
                res += count[k]
        return res

```

**# 2.Review**
> 阅读并点评至少一篇英文技术文章 
主要是 Python ABC
> https://www.python.org/dev/peps/pep-3119/

**# 3.Tip**
> 学习至少一个技术技巧  
* 熟悉了 Celery work loop

**# 4.Share**
> 分享一篇有观点和思考的技术文章  
本周输出 （本周没有输出，不过看 Celery 源码比较多，整理的导图太大了，后面拆分一下，再输出吧
