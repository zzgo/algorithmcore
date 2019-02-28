快速排序的核心思想，找到一个哨兵，这个哨兵一般就是从i=0开始，让这个哨兵与后面的每一个元素比较，凡是比这个元素小的，改变这个哨兵的下标为当前元素的下标，然后继续查找，知道数组中的最后一个元素。然后将此事i位置数与这个哨兵的下标值进行交换，也就是找到一个元素在这个数组是最小的哪一个，然后把它放到i位置来。

```java
public class SelectSort {
    public static void sort(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            int min = i;
            for (int j = i; j < nums.length; j++) {
                if (less(nums[min], nums[j]))
                    min = j;
            }
            exch(nums, i, min);
        }
    }

    public static void main(String[] args) {
        int[] nums = getNums();
        sort(nums);
        print(nums);
    }
}
```



