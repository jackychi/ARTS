# 2019-04-14
**# 1.Algorithm**
> 每周至少做一个 leetcode 的算法题  

https://leetcode.com/problems/search-a-2d-matrix-ii/
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:
Integers in each row are sorted in ascending from left to right.
Integers in each column are sorted in ascending from top to bottom.
两种解题思路：
1. O(mlogN) 二分
2. O(m+n) 从右上角开始找，如果大于 x 就向左走，如果小于 x 就向下走
```
class Solution:
    def searchMatrix1(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        row_count = len(matrix)
        if row_count <= 0:
            return False
        col_count = len(matrix[0])
        if col_count <= 0:
            return False
        for r in range(row_count):
            if self.binary_search(matrix[r], target):
                return True
        return False

    def binary_search(self, l, x):
        start = 0
        end = len(l) - 1
        while start <= end:
            mid = (start + end) // 2
            if l[mid] == x:
                return True
            elif l[mid] > x:
                end = mid - 1
            elif l[mid] < x:
                start = mid + 1
        return False

    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        row_count = len(matrix)
        if row_count <= 0:
            return False
        col_count = len(matrix[0])
        if col_count <= 0:
            return False
        r, c = 0, col_count - 1
        while r < row_count and c >= 0:
            if matrix[r][c] == target:
                return True
            elif matrix[r][c] > target:
                c -= 1
            elif matrix[r][c] < target:
                r += 1
        return False

```


**# 2.Review**
> 阅读并点评至少一篇英文技术文章 
同时读了好几篇，主要是 PEP-205
关于 Python 的 weakref

**# 3.Tip**
> 学习至少一个技术技巧  
* 熟悉了 Celery 的启动过程

**# 4.Share**
> 分享一篇有观点和思考的技术文章  
本周输出 （本周没有输出，贴一个以前的输出吧）


# Go 的测试
我自己在接触一门新语言的时候，总是尽早的去了解这门语言的 UnitTest 相关信息，这样可以写一个函数，就能很方便的跑起来看看效果了，非常爽，非常省时间、精力。

Go 的测试简直太方便了，而且测试在 Go 的设计中也是处于一个比较重要的地位。

## 背景
我写了一段小函数
```go
func add(a, b int) int {
	return a - b
}

func sub(a, b int) int {
	return a - b
}
```

> flag: 这么简单的功能，一定不会出错吧。
那就跑一下吧，很多人的做法是，写个 main 函数，跑一下：
```go
func main() {
	fmt.Println(add(1, 3))
	fmt.Println(sub(3, 2))
}
```
跑完后看输出的结果。
然后跑完上面的 main 函数就会发现， flag 生效了，add 这个函数有点不对。
赶紧改一下，然后再跑完整的命令。
显然，平时不会有这么小的代码，复现一个问题耗时很久。

## 快速开始
go 的测试，非常简单：
- 测试和源码文件在一个包中
- 测试文件的名字是代码文件名 + "_test.go”
- 测试函数的名字是 “Test” + 函数名，并接受一个 *testing.T 的参数
- 命令行 `go test`

知道上面的就已经可以开始了。

## 多了解一点
go 的测试可以分为：
- Test
	- 接收一个参数 *testing.T
	- 并行测试
- Benchmarks
	- 接收一个参数 *testing.B
	- 串行测试
- Examples
	- 可以在注释中搞点事
		- 以 “Output” 开头，然后跟输出比对
		- 以 “Unordered” 开头，就是忽略输出顺序
		- 没有在注释中搞事，只编译不跑
	- 命名有规范，针对：类型 T ，函数 F ，类型 T 的方法 M ，有
```
func Example() { ... }
func ExampleF() { ... }
func ExampleT() { ... }
func ExampleT_M() { ... }

func Example_suffix() { ... }
func ExampleF_suffix() { ... }
func ExampleT_suffix() { ... }
func ExampleT_M_suffix() { ... }
```
	
## 关于 Examples
在看 Go 的文档 [effective go](https://golang.org/doc/effective_go.html) 时，有这么一段：
```
The  [Go package sources](https://golang.org/src/)  are intended to serve not only as the core library but also as examples of how to use the language. Moreover, many of the packages contain working, self-contained executable examples you can run directly from the  [golang.org](https://golang.org/)  web site, such as  [this one](https://golang.org/pkg/strings/#example_Map)  (if necessary, click on the word "Example" to open it up). If you have a question about how to approach a problem or how something might be implemented, the documentation, code and examples in the library can provide answers, ideas and background.

```
