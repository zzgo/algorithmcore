```java
public class Common {
    public static boolean less(int a, int b) {
        if (a > b)
            return true;
        return false;
    }

    public static void exch(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    public static int[] getNums() {
        return new int[]{0, 1, 5, 4, 9, 6, 3, 2, 8, 7};
    }

    public static void print(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            System.out.print(nums[i]);
        }
    }
}
```



