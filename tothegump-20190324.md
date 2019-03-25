# 2019-03-24
**# 1.Algorithm**
> 每周至少做一个 leetcode 的算法题  

又随机到一个 easy，刚好本周时间不多（好熟悉的话术）
[leetcode](https://leetcode.com/problems/univalued-binary-tree/)
不过下周的是个 hard 难度
> A binary tree is_univalued_if every node in the tree has the same value.  
> Returntrueif and only if the given tree is univalued.  


```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
        
    def isUnivalTree(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if root is None:
            return True
        the_value = root.val
        stack = []

        stack.append(root)

        while(len(stack) > 0):
            node = stack.pop()
            if node.val != the_value:
                return False
            if node.right:
                stack.append(node.right)
            if node.left:
                stack.append(node.left)
        return True

```

**# 2.Review**
> 阅读并点评至少一篇英文技术文章  
[Introducing Faust — Faust 1.5.0 documentation](https://faust.readthedocs.io/en/latest/introduction.html)
Faust 相关，其实主要是为了对接 kafka

**# 3.Tip**
> 学习至少一个技术技巧  
- [ ] 了解了 Faust 这个库 

**# 4.Share**
> 分享一篇有观点和思考的技术文章  
本周输出：
呃。。。没有写完
先这样吧
http://blog.tothegump.com/chinwag/java_class_loader_1.html

