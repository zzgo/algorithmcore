### 1.寻找两个有序数组的中位数

给定两个大小为 m 和 n 的有序（升序）数组 nums1 和 nums2。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O\(log\(m + n\)\)。

你可以假设 nums1 和 nums2 不会同时为空。

**示例 1:**

```java
nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0
```

**示例 2:**

```java
nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5
```

**解题思路1:**

```java
时间复杂度O(max(m,n),与题目的O(log(m + n))不一致
```

有序数组，合并，想到归并排序中的marge算法

```java
public class MargeSort {
    public static double findMod(int nums1[], int nums2[]) {
        int len1 = nums1.length;
        int len2 = nums2.length;
        //合并数组
        int[] temp = new int[len1 + len2];
        int i = 0, j = 0, k = 0;
        //为什么可以这样呢，数组是有序的，
        //A集合元素的A1如果不大于B集合元素的B1，那么 A1<B1，如果A1>B1那么B1就一定会小于A2（A1<A2）
        //所以这样的元素还是有序的
        while (i < len1 && j < len2) {
            if (nums1[i] < nums2[j]) {
                temp[k++] = nums1[i++];
            } else {
                temp[k++] = nums2[j++];
            }
        }
        //合并nums1剩余元素
        while (i < len1) {
            temp[k++] = nums1[i++];
        }
        //合并nums2剩余元素
        while (j < len2) {
            temp[k++] = nums2[j++];
        }

        //判断
        if ((len1 + len2) % 2 == 1)
            return temp[(len1 + len2) / 2];
        return (temp[(len1 + len2) / 2] + temp[(len1 + len2) / 2 - 1]) / 2.0;
    }

    public static void main(String[] args) {
        int[] nums1 = new int[]{1, 3};
        int[] nums2 = new int[]{2, 4};
        System.out.println(findMod(nums1, nums2));
    }
}
```

官方解答

```java
    public static double findMedianSortedArrays(int[] A, int[] B) {
        int m = A.length;
        int n = B.length;
        if (m > n) { // to ensure m<=n
            int[] temp = A;
            A = B;
            B = temp;
            int tmp = m;
            m = n;
            n = tmp;
        }
        int iMin = 0, iMax = m, halfLen = (m + n + 1) / 2;
        while (iMin <= iMax) {
            int i = (iMin + iMax) / 2;
            int j = halfLen - i;
            if (i < iMax && B[j - 1] > A[i]) {
                iMin = i + 1; // i is too small
            } else if (i > iMin && A[i - 1] > B[j]) {
                iMax = i - 1; // i is too big
            } else { // i is perfect
                int maxLeft = 0;
                if (i == 0) {
                    maxLeft = B[j - 1];
                } else if (j == 0) {
                    maxLeft = A[i - 1];
                } else {
                    maxLeft = Math.max(A[i - 1], B[j - 1]);
                }
                if ((m + n) % 2 == 1) {
                    return maxLeft;
                }

                int minRight = 0;
                if (i == m) {
                    minRight = B[j];
                } else if (j == n) {
                    minRight = A[i];
                } else {
                    minRight = Math.min(B[j], A[i]);
                }

                return (maxLeft + minRight) / 2.0;
            }
        }
        return 0.0;
    }
```



