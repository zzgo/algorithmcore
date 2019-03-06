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



