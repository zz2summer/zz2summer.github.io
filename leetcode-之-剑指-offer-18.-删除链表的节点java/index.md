# LeetCode 之 剑指 Offer 18. 删除链表的节点（Java）


[剑指 Offer 18. 删除链表的节点](https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/)，给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。返回删除后的链表的头节点。

<!--more-->

> 版权声明：本文为博主 [渣渣的夏天](https://zz2summer.github.io/) 的原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。 

## 一、题目
[剑指 Offer 18. 删除链表的节点](https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

注意：此题对比原题有改动

示例 1:

```bash
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```

示例 2:

```bash
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```


说明：

- 题目保证链表中节点的值互不相同
- 若使用 C 或 C++ 语言，你不需要 free 或 delete 被删除的节点

来源：力扣（LeetCode）

链接：https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


## 二、解题思路

&emsp;&emsp;节点常规操作，遍历所有节点找到对应待删除的节点。

&emsp;&emsp;每次判断下一个节点是否为待删除节点，如果不是则将当前节点改为下一节点，如果是将当前节点的 next 改为该节点的 next.next 即可，也就是删除了 下一个 next。注意删除节点是头节点、尾结点时的边界情况，当删除头节点时，直接返回 head.next ；当删除尾结点时，则将当前节点的 next 直接改为 null待删除节点的上一节点的。

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
    public ListNode deleteNode(ListNode head, int val) {
        // head node
        if(head.val == val){
            return head.next;
        }else{
            ListNode curNode = head;
            while(curNode.next.val != val){
                curNode = curNode.next;
            }
            if(curNode.next.next == null){
                // end node
                curNode.next = null;
            }else{
                curNode.next = curNode.next.next;
            }
            return head;
        }
    }
}
```

