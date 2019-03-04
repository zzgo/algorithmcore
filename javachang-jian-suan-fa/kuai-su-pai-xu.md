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



