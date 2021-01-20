## No.002 两数相加  
### Add Two Numbers 

* 给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。  
* 请你将两个数相加，并以相同形式返回一个表示和的链表。  
* 你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

```
示例 1：
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
```  
```
示例 2：
输入：l1 = [0], l2 = [0]
输出：[0]
```  
```
示例 3：
输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出：[8,9,9,9,0,0,0,1]
```

> 提示：  
> 1. 每个链表中的节点数在范围 [1, 100] 内  
> 2. 0 <= Node.val <= 9  
> 3. 题目数据保证列表表示的数字不含前导零  

### 结果代码  
*  运行时间：2 ms
*  内存消耗：38.6 MB   

```
public static void main(String[] args) {
    ListNode n3 = new ListNode(3);
    ListNode n2 = new ListNode(4, n3);
    ListNode n1 = new ListNode(2, n2);

    ListNode x3 = new ListNode(4);
    ListNode x2 = new ListNode(6, x3);
    ListNode x1 = new ListNode(5, x2);

    ListNode result = addTwoNumbers(n1, x1);
    System.out.println(result);
}

public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    if (l1 == null && l2 == null) {
        return null;
    }
    // 哨兵节点
    ListNode firstNode = new ListNode();

    ListNode resultNode = firstNode;
    int extra = 0;
    while (l1 != null || l2 != null) {
        int sum = extra;
        // 分别进行判空，然后计算
        if (l1 != null) {
            sum = sum + l1.val;
            l1 = l1.next;
        }
        if (l2 != null) {
            sum = sum + l2.val;
            l2 = l2.next;
        }
        extra = sum / 10;
        resultNode.next = new ListNode(sum % 10);
        resultNode = resultNode.next;
    }
    // 在计算全部完成后如果有多余的1，进位
    if (extra > 0) {
        resultNode.next = new ListNode(extra);
    }
    return firstNode.next;
}

public static class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}
```

### English  
* You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.  
* You may assume the two numbers do not contain any leading zero, except the number 0 itself.

```
Example 1:
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```  
```
Example 2:
Input: l1 = [0], l2 = [0]
Output: [0]
```  
```
Example 3:
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

> Constraints:  
> 1. The number of nodes in each linked list is in the range [1, 100].  
> 2. 0 <= Node.val <= 9  
> 3. It is guaranteed that the list represents a number that does not have leading zeros.

