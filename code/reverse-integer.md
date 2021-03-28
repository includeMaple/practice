
# 概要
https://leetcode-cn.com/problems/reverse-integer/

## 思路

思路：

1. 练习方法的运用，将数字当字符串处理，如下面的JavaScript
1. 正常运算处理，如下面的c++

注意：

1. 边界值-2^31 <= x <= 2^31 - 1，输出校验

# C++

如果使用int而不是long，overflow

```c++
class Solution {
public:
    int reverse(int x) {
        long n = 0;
        while (x)
        {
            n = n * 10 + x % 10;
            x /= 10;
        }
        return n > INT_MAX || n < INT_MIN ? 0 : n;
    }
};
```

# javascript

练习方法运用。

```javascript
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
  // init
  let start = x < 0 ? 1: 0
  // deal as string
  let str = String(x).slice(start)
  let num = Number(str.split('').reverse().join(''))
  if (start===1) num =  -num;
  return (num<-Math.pow(2, 31)|| num>Math.pow(2, 31)-1) ? 0: num
};
```

# python

python2和python3通用，python中取模结果和其他语言不太一样。

```python
class Solution(object):

    def reverse(self, x):
      num = 0
      flag = False
      if x<0:
        flag = True
        x = -x
      while x:
        num = 10*num + x % 10
        x //= 10
      if flag:
        num = -num
      if (num<-2**31 or num>2**31-1):
        return 0
      return num
```

如果python也使用方法：

```python
class Solution:
    def reverse(self, x: int) -> int:
        tmp = int((str(x) if x > 0 else str(-x) + "-")[::-1])
        return tmp if -2 ** 31 < tmp < 2 ** 31 - 1 else 0
```
