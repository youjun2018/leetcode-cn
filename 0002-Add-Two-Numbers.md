# 两数相加 Add Two Numbers


## 题目描述
给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807


## 解题思路
1. 题目涉及到链表，因此需要两个链表指针 p1，p2 来指向原来的链表 l1，l2。
2. 由于函数返回值类型是 ListNode，因此需要建立一个新的链表 returnHead。（使用原链表的以节省空间的方法后面再说）此外还需要为新建的链表节点指定指针，此处设为 curr。
3. 题目牵涉到进位，设置 int flag 为进位标志，如果有进位 flag 为 1，如果没有进位，flag 为 0。题目涉及到求和，设置 int sum 为计算的和。
4. 循环遍历两个链表，直到遍历完其中较短一条链表为止（也有可能两条链表同样长？）。在循环体中，sum = flag + p1.val + p2.val，求和需要需要连同进位一起算。判断 sum >= 10 是否成立。如果成立，则新建链表节点 new ListNode(sum % 10)，并使用 curr.next 指向它，并使 flag 为 0。如果 sum >= 10 不成立，则新建立链表节点 new ListNode(sum) 并使用 curr.next 指向它，并使 flag 为 0。别忘设置 p1,p2,current 指向其后一个链表节点。
5. 上述循环结束后，会有三种可能性，p1 为 null, p2 不为 null; p1 不为 null，p2 为 null；p1 p2 都为 null。
6. 若 p1 为 null, p2 不为 null，用 p2 后面的链表节点创建 curr 链表。同时注意求和时带上 flag。
7. 若 p1 不为 null，p2 为 null，用 p1 后面的链表节点创建 curr 链表。同时注意求和时带上 flag。
8. 最后要判断 flag 是否为 1。如果 flag 为 1，则要创建一个链表节点，存放 flag 值。
9. 返回 curr.next。因为 curr 链表第一个节点的值为 0。


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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode returnHead = new ListNode(0);
        ListNode p1 = l1;
        ListNode p2 = l2;
        ListNode curr = returnHead;
        int flag = 0;
        int sum = 0;

        while(p1 != null && p2 != null){
            sum = flag + p1.val + p2.val;
            if(sum >= 10){
                curr.next = new ListNode(sum % 10);
                flag = 1;
            }
            else{
                curr.next = new ListNode(sum);
                flag = 0;
            }

            p1 = p1.next;
            p2 = p2.next;
            curr = curr.next;
        }

        if(p1 != null) {
            while(p1 != null) {
                sum = flag + p1.val;
                if(sum >= 10) {
                    curr.next = new ListNode(sum % 10);
                    flag = 1;
                }
                else {
                    curr.next = new ListNode(sum);
                    flag = 0;
                }     
                curr = curr.next;
                p1 = p1.next;
            }
        }

        if(p2 != null) {
            while(p2 != null) {
                sum = flag + p2.val;
                if(sum >= 10) {
                    curr.next = new ListNode(sum % 10);
                    flag = 1;
                }
                else {
                    curr.next = new ListNode(sum);
                    flag = 0;
                }     
                curr = curr.next;
                p2 = p2.next;
            }
        }

        if(flag != 0) {
            curr.next = new ListNode(flag);
            curr = curr.next;
            flag = 0;
        }

        return returnHead.next;
    }
}
```

##### 自己 java 代码分析
###### 时间复杂度
1. 在 leetcode-cn.com 提交用时 11 ms，战胜 100.00% 的 java 提交记录。提交日期：20190401。
2. 在 leetcode.com 提交用时 2 ms，战胜 99.15% 的提交记录。提交日期：20190401。

时间复杂度：O(max(m,n))，假设 m 和 n 分别表示 l1 和 l2 的长度，上面算法最多重复 max(m,n) 次。

###### 空间复杂度
1. 在 leetcode-cn.com 提交占用空间 44.4 MB，战胜 38.47% 的 java 提交记录。提交日期：20190401。
2. 在 leetcode.com 提交占用空间 46.1 MB，战胜 54.25% 的提交记录。提交日期：20190401。

空间复杂度：O(max(m,n))，新列表的长度最多为 max(m,n) + 1.


### 大神的代码
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummyHead = new ListNode(0);
        ListNode p = l1, q = l2, curr = dummyHead;
        int carry = 0;
        while (p != null || q != null) {
            int x = (p != null) ? p.val : 0;
            int y = (q != null) ? q.val : 0;
            int sum = carry + x + y;
            carry = sum / 10;
            curr.next = new ListNode(sum % 10);
            curr = curr.next;
            if (p != null) p = p.next;
            if (q != null) q = q.next;
        }
        if (carry > 0) {
            curr.next = new ListNode(carry);
        }
        return dummyHead.next;
    }
}
```

##### 大神 java 代码分析
###### 时间复杂度
1. 在 leetcode-cn.com 提交用时 11 ms，战胜 100.00% 的 java 提交记录。提交日期：20190401。

###### 空间复杂度
1. 在 leetcode-cn.com 提交占用空间 44.4 MB，战胜 38.47% 的 java 提交记录。提交日期：20190401。

大神的代码和我写的代码的思路很相似，但是大神的代码写的好简洁，很漂亮。它用变量 x 和 y 来保存两个链表中节点的值，然后使用三目运算符来计算 x 和 y 值，这样就可以屏蔽链表为空的情况。


## 总结归纳
1. Java 中链表是类，要使用 . 运算符来访问内部变量。C++ 中使用 -> 运算符来访问链表节点值。


## 遇到的问题
1. 打算使用 函数中的 l1 变量，这样空间复杂度为 O(max(m,n))。修改大神的代码使用链表 l1 存放结果。
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //ListNode dummyHead = new ListNode(0);
        ListNode dummyHead = l1;
        ListNode p = l1, q = l2;
        int carry = 0;
        ListNode pp = l1;
        ListNode qq = l2;
        while (p != null || q != null) {
            int x = (p != null) ? p.val : 0;
            int y = (q != null) ? q.val : 0;
            int sum = carry + x + y;
            carry = sum / 10;
            p.val = sum % 10;

            if (p.next == null) pp = p;
            // if (q.next == null) qq = q;

            if (p != null) p = p.next;
            if (q != null) q = q.next;

            if (p == null)
            {
                pp.next = q;
                p = q;
                q = null;
            }

        }

        if (carry > 0) {
            pp.next = new ListNode(carry);
        }
        return dummyHead;
    }
}
```
期初修改的代码会报错误 "java.lang.NullPointerException"。原因是空指针使用了 next 变量，例 p.next 会出错当 p 为空的话。大神的代码重新建立一个链表，所以就不用考虑 p 为空的情况。

```Java
if (p != null) p = p.next;
if (q != null) q = q.next;
```

当链表遍历到最后一个节点时，这两行代码执行后 p,q 都是 null。需要额外的变量来指定链表尾部。

此外程序运行时间有时是不准确的，同样的代码，提交多次用时都是不一样的。

## 参考链接
[Java数据结构和算法（七）——链表](https://www.cnblogs.com/ysocean/p/7928988.html)

[Java LinkedList类链表](https://www.yiibai.com/java/java_linkedlist_class.html)


## 知识延伸






end of page
