快速排序的核心思想，找到一个哨兵，这个哨兵一般就是从i=0开始，让这个哨兵与后面的每一个元素比较，凡是比这个元素小的，改变这个哨兵的下标为当前元素的下标，然后继续查找，知道数组中的最后一个元素。然后将此事i位置数与这个哨兵的下标值进行交换，也就是找到一个元素在这个数组是最小的哪一个，然后把它放到i位置来。

```java
import static com.zachary.Common.*;

public class QuickSort {
    public static void sort(int[] nums) {
        sort(nums, 0, nums.length - 1);
    }

    private static void sort(int[] nums, int low, int high) {
        int pos;
        if (low < high) {
            pos = pos(nums, low, high);
            sort(nums, 0, pos);
            sort(nums, pos + 1, high);
        }
    }

    private static int pos(int[] nums, int low, int high) {
        int temp = nums[low];
        while (low < high) {
            while (low < high && nums[high] >= temp)
                high--;
            if (low < high)
                nums[low++] = nums[high];
            while (low < high && nums[low] <= temp)
                low++;
            if (low < high)
                nums[high--] = nums[low];

        }
        nums[low] = temp;
        return low;
    }

    public static void main(String[] args) {
        int[] nums = getNums();
        sort(nums);
        print(nums);
    }
}
```



