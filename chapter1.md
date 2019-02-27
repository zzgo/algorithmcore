### 1.两数之和

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

* 给定 nums = \[2, 7, 11, 15\], target = 9
* 因为 nums\[0\] + nums\[1\] = 2 + 7 = 9

```java
public int[] addSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            int n = target - num;
            if (map.containsKey(n)) {
                return new int[]{map.get(n), i};
            }
            map.put(num, i);
        }
        return null;
    }
```

### 2.两数相加

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

```java
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

链表操作

```java
public class Ch01 {
    public static ListNode addTwoNumbers(ListNode node1, ListNode node2) {
        ListNode target = new ListNode(0, null);
        //节点指向游标，关键思想
        ListNode curr = target;
        int carry = 0;
        //确保两个node都不为空
        while (node1 != null || node2 != null) {
            //保证长度不一样的情况
            int x = (node1 != null) ? node1.val : 0;
            int y = (node2 != null) ? node2.val : 0;
            //进行相加操作
            int sum = x + y + carry;
            //计算进位值
            carry = sum / 10;
            //计算余数值
            curr.next = new ListNode(sum % 10, null);
            //指向下一个节点
            curr = curr.next;
            //node1.next不为为空
            node1 = (node1 != null) ? node1.next : null;
            node2 = (node1 != null) ? node2.next : null;
        }

        if (carry > 0) {
            curr.next = new ListNode(carry, null);
        }
        return target.next;
    }

    public static void main(String[] args) {
//        输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
//        输出：7 -> 0 -> 8
//        原因：342 + 465 = 807

        ListNode left = new ListNode(2, null);
        ListNode left_1 = new ListNode(4, null);
        left.next = left_1;
        ListNode left_2 = new ListNode(3, null);
        left_1.next = left_2;

        ListNode right = new ListNode(5, null);
        ListNode right_1 = new ListNode(6, null);
        right.next = right_1;
        ListNode right_2 = new ListNode(4, null);
        right_1.next = right_2;
        ListNode node = addTwoNumbers(left, right);

        while (left != null) {
            System.out.print(left.val + " -> ");
            left = left.next;
        }
        System.out.println();
        while (right != null) {
            System.out.print(right.val + " -> ");
            right = right.next;
        }
        System.out.println();
        while (node != null) {
            System.out.print(node.val + " -> ");
            node = node.next;
        }

    }

}
```

ListNode.java

```java
public class ListNode {
    protected int val;
    protected ListNode next;

    public ListNode() {
    }

    public ListNode(int val, ListNode next) {
        this.val = val;
        this.next = next;
    }

    public int getVal() {
        return val;
    }

    public void setVal(int val) {
        this.val = val;
    }

    public ListNode getNext() {
        return next;
    }

    public void setNext(ListNode next) {
        this.next = next;
    }
}
```

链表的反序输出

```java
public static void print(ListNode node) {
    // 先遍历到最尾部，然后在一步一步的向前输出
    if (node.next != null) {
        print(node.next);
    }
    System.out.print(node.val);
}
```

大数相加也可以采用该链表的形式，但是长度过长，会出现java.lang.StackOverflowError

