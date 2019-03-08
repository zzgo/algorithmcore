### 最长公共前缀

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。

**示例 1:**

```
输入: 
["flower","flow","flight"]

输出:
 "fl"
```

**示例 2:**

```
输入: 
["dog","racecar","car"]

输出:
 ""

解释:
 输入不存在公共前缀。
```

**说明:**

所有输入只包含小写字母 `a-z` 。

```java
    // 垃圾代码
    public static String longestCommonPrefix(String[] strs) {
        int len;
        if (null == strs || (len = strs.length) == 0) return "";
        for (int i = 0; i < len - 1; i++) {
            if (strs[0].length() > strs[i + 1].length()) {
                String s = strs[0];
                strs[0] = strs[i + 1];
                strs[i + 1] = s;
            }
        }
        if ("".equals(strs[0])) return "";
        String sRet = "";
        for (int i = 0; i < strs[0].length(); i++) {
            String s = strs[0].substring(0, i + 1);
            boolean bRet = true;
            for (int j = 1; j < len; j++) {
                if (!strs[j].startsWith(s)) {
                    bRet = false;
                    break;
                }
            }
            if (bRet) {
                sRet = s;
            }
        }
        return sRet;
    }

    //好好看看别人写的代码
    public static String longestCommonPrefix2(String[] strs) {
        int len;
        if (null == strs || (len = strs.length) == 0) return "";
        // 可以不需要这段代码。
        for (int i = 0; i < len - 1; i++) {
            if (strs[0].length() > strs[i + 1].length()) {
                String s = strs[0];
                strs[0] = strs[i + 1];
                strs[i + 1] = s;
            }
        }
        if ("".equals(strs[0])) return "";
        String str = strs[0];
        //好好看看别人写的代码
        for (int i = 1; i < len; i++) {
            //while是找到 两个字符之间的最长前缀
            while (!strs[i].startsWith(str)) {
                if (str.length() > 1) {
                    //首先是从最长开始，然后自减
                    str = str.substring(0, str.length() - 1);
                } else {
                    return "";
                }
            }
        }
        return str;
    }
```

### 三数之和

给定一个包含_n_个整数的数组 `nums`，判断 `nums` 中是否存在三个元素_a，b，c ，_使得 \_a + b + c =\_0 ？找出所有满足条件且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

```
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

代码：

```java
public class T15 {
    public static List<List<Integer>> threeSum(int[] nums) {
        int len;
        if (null == nums || (len = nums.length) == 0)
            return null;
        List<List<Integer>> lists = new ArrayList<>();
        Arrays.sort(nums);
        for (int c = len - 1; c >= 2; ) {
            for (int a = 0, b = c - 1; a < b; ) {
                int temp_sum = nums[a] + nums[b];
                if (temp_sum < -nums[c]) {
                    ++a;
                } else if (temp_sum > -nums[c]) {
                    --b;
                } else {
                    List<Integer> list = Arrays.asList(nums[a], nums[b], nums[c]);
                    lists.add(list);
                    do {
                        ++a;
                    } while (a < b && nums[a - 1] == nums[a]);
                    do {
                        --b;
                    } while (a < b && nums[b + 1] == nums[b]);
                }
            }
            do {
                --c;
            } while (c >= 2 && nums[c + 1] == nums[c]);

        }
        return lists;
    }

    public static void main(String[] args) {
        System.out.println(Arrays.asList(threeSum(new int[]{-1, 0, 1, 2, -1, -4})));
    }
}
```

二

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        if (nums.length < 3)
                return Collections.emptyList();
            List<List<Integer>> res = new ArrayList<>();
            int minValue = Integer.MAX_VALUE;
            int maxValue = Integer.MIN_VALUE;
            int negSize = 0;
            int posSize = 0;
            int zeroSize = 0;
            for (int v : nums) {
                if (v < minValue)
                    minValue = v;
                if (v > maxValue)
                    maxValue = v;
                if (v > 0)
                    posSize++;
                else if (v < 0)
                    negSize++;
                else
                    zeroSize++;
            }
            if (zeroSize >= 3)
                res.add(Arrays.asList(0, 0, 0));
            if (negSize == 0 || posSize == 0)
                return res;
            if (minValue * 2 + maxValue > 0)
                maxValue = -minValue * 2;
            else if (maxValue * 2 + minValue < 0)
                minValue = -maxValue * 2;

            int[] map = new int[maxValue - minValue + 1];
            int[] negs = new int[negSize];
            int[] poses = new int[posSize];
            negSize = 0;
            posSize = 0;
            for (int v : nums) {
                if (v >= minValue && v <= maxValue) {
                    if (map[v - minValue]++ == 0) {
                        if (v > 0)
                            poses[posSize++] = v;
                        else if (v < 0)
                            negs[negSize++] = v;
                    }
                }
            }
            Arrays.sort(poses, 0, posSize);
            Arrays.sort(negs, 0, negSize);
            int basej = 0;
            for (int i = negSize - 1; i >= 0; i--) {
                int nv = negs[i];
                int minp = (-nv) >>> 1;
                while (basej < posSize && poses[basej] < minp)
                    basej++;
                for (int j = basej; j < posSize; j++) {
                    int pv = poses[j];
                    int cv = 0 - nv - pv;
                    if (cv >= nv && cv <= pv) {
                        if (cv == nv) {
                            if (map[nv - minValue] > 1)
                                res.add(Arrays.asList(nv, nv, pv));
                        } else if (cv == pv) {
                            if (map[pv - minValue] > 1)
                                res.add(Arrays.asList(nv, pv, pv));
                        } else {
                            if (map[cv - minValue] > 0)
                                res.add(Arrays.asList(nv, cv, pv));
                        }
                    } else if (cv < nv)
                        break;
                }
            }
            return res;

    }
}
```



