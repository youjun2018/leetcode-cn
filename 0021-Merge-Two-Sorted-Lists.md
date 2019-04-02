# 合并两个有序链表 Merge Two Sorted Lists

## 题目描述
将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

示例：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4


## 解题思路
1. 创建一个返回链表的头结点 retList，并创建一个指向返回链表的尾结点 curList。
2. 循环遍历 l1 和 l2，若 l1 和 l2 都不为空时，比较 l1 和 l2 指向节点值的大小，并让 curList 指向值较小的节点，并且让指向较小节点原链表的指针向后移。
3. 跳出循环后，有三种可能，l1 为空，l2 不为空；l1 不为空，l2 为空；l1 为空，l2 为空。若 l1 为空，则把 l2 赋值给 curList；否则，把 l1 赋值给 curList。


## 实现代码
### 自己的代码
#### java 代码
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode retList = new ListNode(0);
        ListNode curList = retList;

        while(l1 != null && l2 != null)
        {
            curList.next = (l1.val <= l2.val)? l1 : l2;
            if(l1.val <= l2.val) {
                curList.next = l1;
                l1 = l1.next;
            } else {
                curList.next = l2;
                l2 = l2.next;
            }

            curList = curList.next;
        }

        if(l1 != null)
        {
            curList.next = l1;
        }
        else
        {
            curList.next = l2;
        }
        return retList.next;
    }
}
```

##### 自己 java 代码分析
###### 时间复杂度
时间复杂度为 O(m+n)，假设 m，n 分别为 l1 和 l2 的长度。


###### 空间复杂度
空间复杂度为 O(1)。


## 总结归纳
自己的解法是额外创建了一个节点。如果不创建节点的话，代码会很冗肿，不清晰。



end of this page
