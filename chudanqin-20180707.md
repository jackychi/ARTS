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
    while (x != 0) { // Zero returns zero.
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



## 知识点

I have a basic understanding of 'Overflow', and there is another concept 'Underflow' I have never heard.

### Overflow

> The condition that occurs when a calculation produces a result that is greater in magnitude than that which a given register or storage location can store or represent.
>
> The C standard suggests: A computation involving unsigned operands can never overflow, because a result that cannot be represented by the resulting unsigned integer type is reduced modulo the number that is one greater than the largest value that can be represented by the resulting type.
>
> C 标准中：有符号整数会溢出，OF 置为 1，其结果是未定义行为。无符号整数不会溢出，做加法，超出表示范围，就会进位做减法；不够减，就会借位；此时，CF 置为 1。

### Underflow

> The condition in a computer program that can occur when the true result of a floating point operation is smaller in magnitude (that is, closer to zero) than the smallest value representable as a normal floating point number in the target datatype.
>
> 太小了而没法表示。
>
> float x = 1e-30; x /= 1e20; // Underflow!