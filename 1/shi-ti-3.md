### 1、回文数

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

**示例 1:**

```
输入:
 121

输出:
 true
```

**示例 2:**

```
输入:
 -121

输出:
 false

解释:
 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```

**示例 3:**

```
输入:
 10

输出:
 false

解释:
 从右向左读, 为 01 。因此它不是一个回文数。
```

**进阶:**

你能不将整数转为字符串来解决这个问题吗？

解题思路：是负数不是回文数，末尾为0不是回文数（首数字肯定不是0，除0数字外）

```java
    //方法1 取余
    public static boolean isPalindrome2(int x) {
        if (x >= 0 && x < 10)
            return true;
        if (x < 0 || x % 10 == 0)
            return false;
        int ret = 0;
        int x0 = x;
        while (x != 0) {
            ret = ret * 10 + x % 10;
            x = x / 10;
        }
        if (x0 == ret)
            return true;
        return false;
    }

    //方法2 二分
    public static boolean isPalindrome(int x) {
        String str = String.valueOf(x);
        char[] chars = str.toCharArray();
        int len;
        if ((len = chars.length) == 1)
            return true;
        int low = 0;
        int high = len - 1;
        while (chars[low++] == chars[high--]) {
            if (low > high)
                return true;
        }
        return false;
    }
```



