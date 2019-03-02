1、整数反转

给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

**示例 1:**

```java
输入:
 123
输出:
 321
```

** 示例 2:**

```java
输入:
 -123
输出:
 -321
```

**示例 3:**

```java
输入:
 120
输出:
 21
```

解题思路1：

变成字符串反转，有点蠢。

```java
public static int reverse(int x) {
        String s = "";
        int pre = 0;
        if (x < 0) {
            x = -x;
            pre = -1;
        }
        char[] c = (x + "").toCharArray();
        for (int i = c.length - 1; i >= 0; i--) {
            if (c[c.length - 1] == 0) continue;
            s = s + c[i];
        }
        try {
            if (pre == 0)
                return Integer.parseInt(s);
            return -Integer.parseInt(s);
        } catch (Exception e) {

        }
        return 0;
}
```

解题思路2：

直接利用取余法

```java
public static int reverse(int x) {
        long ret = 0;
        while (x != 0) {
                //反转 思路很妙
                ret = ret * 10 + x % 10;
                x = x / 10;
                if (ret > Integer.MAX_VALUE || ret < Integer.MIN_VALUE)
                    return 0;
        }
        return (int) ret;
}
```



