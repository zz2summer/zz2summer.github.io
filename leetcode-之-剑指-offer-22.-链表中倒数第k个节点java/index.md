# LeetCode 之 剑指 Offer 22. 链表中倒数第k个节点（Java）


[剑指 Offer 22. 链表中倒数第k个节点](https://leetcode.cn/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)，输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

<!--more-->

> 版权声明：本文为博主 [渣渣的夏天](https://zz2summer.github.io/) 的原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。 

## 一、题目
[剑指 Offer 22. 链表中倒数第k个节点](https://leetcode.cn/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。



示例：

```bash
给定一个链表: 1->2->3->4->5, 和 k = 2.
返回链表 4->5.
```

来源：力扣（LeetCode）

链接：https://leetcode.cn/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


## 二、解题思路

&emsp;&emsp;最朴素的方法先遍历一遍得到链表长度 n，然后再遍历一遍得到 n-k+1 节点（倒数第k个）。

&emsp;&emsp;将 O(n^2) 转成 O(n) 可以考虑双指针，此处即可以用快慢指针。第一个指针先走 k-1 步，后面两个指针一起走。当第一个指针走到末端时，另一个指针刚好 n-k+1 个节点，即倒数第 k 个节点。

## 三、代码
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
    public ListNode getKthFromEnd(ListNode head, int k) {
        if(head == null || k < 1){
            return new ListNode();
        }
        ListNode start = head;
        ListNode end = head;
        int count = 1;
        while(end.next != null){
            if(count > k-1){
                start = start.next;
            }
            end = end.next;
            count++;
        }
        return start;
    }
}
```

