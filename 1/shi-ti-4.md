### 1、接雨水

给定 _n_个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

![](/assets/231478sdhaj.png)

上面是由数组 \[0,1,0,2,1,0,1,3,2,1,2,1\] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 **感谢 Marcos**贡献此图。

**示例:**

```
输入:
 [0,1,0,2,1,0,1,3,2,1,2,1]

输出:
 6
```

解题思路：



```java
        //错误方法，未实现 
       public int trap(int[] height) {
        int len = 0;
        if (null == height && (len = height.length) == 0)
            return 0;
        int low = 0;
        int high = len - 1;
        while (height[low] < height[++low] && low < high) ;
        while (height[high] < height[--high] && high > 0) ;
        low = low - 1;
        high = high + 1;
        int low0 = low;
        int high0 = high;
        int max = 0;
        if (low == high)
            return 0;
        while (height[low] > height[++low] && low < len - 1) {
            for (int i = low0; i < low; i++) {
                if (height[i] >= height[low0]) {
                    max = max + 0;
                } else {
                    max = max + height[low0] - height[i];
                }
            }
        }


        for (int i = high; i <= low; i++) {

        }


        return 0;
    }
    // 方法2    
    public static int trap2(int[] height) {
        int len = 0;
        if (null == height || (len = height.length) == 0)
            return 0;
        int[] left = new int[len];
        int[] right = new int[len];

        for (int i = 1; i < len; i++) {
            left[i] = Math.max(left[i - 1], height[i - 1]);
        }
        for (int i = len - 2; i >= 0; i--) {
            right[i] = Math.max(right[i + 1], height[i + 1]);
        }
        int water = 0;
        for (int i = 0; i < len; i++) {
            int level = Math.min(left[i], right[i]);
            water += Math.max(0, level - height[i]);
        }
        return water;
    }
    // 方法3
    public static int trap3(int[] height) {
        if (height.length < 3) {
            return 0;
        }
        return find(height, 0, height.length - 1);
    }

    public static int find(int[] height, int start, int end) {
        if (end - start < 2) {//递归的终点
            return 0;
        }
        int max = -1, tmp = -1, min_two = Math.min(height[start], height[end]), sum = 0;
        ;
        for (int i = start + 1; i < end; i++) {
            //这一句写在哪里都行
            sum = sum + (min_two - height[i]);
            if (height[i] > max) {
                max = height[i];
                tmp = i;
            }
        }

        if (max < min_two) {//上面的加法其实应该在这里，转移到上面和在这里其实都一样
            //sum=sum+(min_two-height[i]);
            return sum;
        } else {//其实这里还可以优化一下当中间的max值等于start或者end的时候，当它等于start,那么直接计算即可，不用进行下一次递归，因为下一次递归会再扫描一遍
            return find(height, start, tmp) + find(height, tmp, end);
        }
    }
```



