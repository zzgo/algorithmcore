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

### 2、盛最多水的容器

给定_n_个非负整数_a_1，_a_2，...，_a_n，每个数代表坐标中的一个点 \(_i_, _ai_\) 。在坐标内画_n_条垂直线，垂直线_i_ 的两个端点分别为 \(_i_, _ai_\) 和 \(_i_, 0\)。找出其中的两条线，使得它们与 _x_ 轴共同构成的容器可以容纳最多的水。

**说明：**你不能倾斜容器，且 _n_ 的值至少为 2。

![](/assets/32478hefhesj.png)

**示例:**

```
输入:
 [1,8,6,2,5,4,8,3,7]

输出:
 49
```

解题思路1：暴力法

从零开始计算，比较两个柱子的高度，然后取小值剩以之间的间距，然后与max比较。

解题思路2：指针法

记录低位low和高位high，low&lt;high 前提下，比较两个的值，并且去小值乘以之间距离，并有小于的一方是低位则向前寻找，如果小于自己的值则跳过，小于一方为高位则向后寻找，如果小于自己的值则跳过，最后与max比较，进行替换

```java
    //暴力法
    public static int maxArea(int[] height) {
        int max = 0;
        int len = height.length;
        int ret = 0;
        for (int i = 0; i < len; i++) {
            for (int j = i + 1; j < len; j++) {
                // 向后依次计算，比较最大值
                if (height[i] < height[j])
                    ret = height[i] * (j - i);
                else
                    ret = height[j] * (j - i);
                if (ret > max)
                    max = ret;
            }
        }
        return max;
    }

    //两端指针法
    public static int maxArea2(int[] height) {
        int max = 0, ret = 0, temp = 0;
        // 一个指向低位，一个指向高位
        int low = 0, high = height.length - 1;
        while (low < high) {
            //低位小于高位，按低位计算
            if (height[low] < height[high]) {
                ret = height[low] * (high - low);
                temp = height[low];
                //如果低位向前寻找小于等于自己的，跳过
                while (height[++low] < temp && low < high) ;
            } else {
                //低位大于高位，取高位计算
                ret = height[high] * (high - low);
                temp = height[high];
                //高位向后寻找小于等于自己的跳过
                while (height[--high] < temp && low < high) ;
            }
            if (ret > max)
                max = ret;
        }
        return max;
    }
```



