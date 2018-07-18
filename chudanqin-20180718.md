## 再接再厉

### LeetCode

<a href='https://leetcode.com/problems/palindrome-number/description/'>Palindrome Number</a>

> Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

``` c
bool isPalindrome(int x) {
    int digits[10] = {0, }; // saving each digit of x
    int n = 0;
    while (x > 0) { // only test positive numbers
        digits[n] = x % 10;
        n++;
        x = x / 10;
    }
    for (int i = 0, j = n - 1; i <= j; ) { // test equality for every head and tail, and then move forward/back
        int a = digits[i];
        int b = digits[j];
        if (a != b) {
            return 0;
        }
        i++; j --;
    }
    return n > 0 || x >= 0; // 1. n > 0 or 2. n <= 0 and x >= 0
}
```

### 英文阅读

<a href='https://mp.weixin.qq.com/s/XGphfIs3kYJDwKd7e-AvLA'>来自于比尔·盖茨的公众号</a>

What I learnt from it? The World Is Flat!