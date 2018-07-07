## 万事开头难

先尝试最容易坚持的，刷 LeetCode，从简单的题目开始吧。

<a href=https://leetcode.com/submissions/detail/162564163/>Reverse Integer</a>

```c
int reverse(int x) {
    /** 
    * INT_MAX = 2147483647, INT_MIN = -2147483648.
    * A positive number is always positive in the progress of reversing.
    * A negative number is always negative in the progress of reversing.
    */
    int rx = 0;
    int max = INT_MAX / 10;
    int min = INT_MIN / 10;
    while (x != 0) { Zero returns zero.
        if (rx > max) { // rx * 10 will be great than INT_MAX, which causes overflow
            return 0;
        }
        if (rx < min) { // rx * 10 will be less than INT_MIN, which causes overflow
            return 0;
        }
        int mod = x % 10;
        if (rx == max && mod > 7) { // rx = 2147483640, so overflown if mod > 7
            return 0;
        }
        if (rx == min && mod < -8) { // rx = -2147483640, so overflown if mod < -8
            return 0;
        }
        rx = rx * 10 + mod;
        x = x / 10;
    }
    return rx;
}
```







