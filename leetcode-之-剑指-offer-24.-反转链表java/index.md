# LeetCode 之 剑指 Offer 24. 反转链表（Java）


[剑指 Offer 24. 反转链表](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/)，定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

<!--more-->

> 版权声明：本文为博主 [渣渣的夏天](https://zz2summer.github.io/) 的原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。 

## 一、题目
[剑指 Offer 24. 反转链表](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/)

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

示例:

```bash
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```


限制：

1. 0 <= 节点个数 <= 5000

来源：力扣（LeetCode）

链接：https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


## 二、解题思路

&emsp;&emsp;反转链表因为没办法知道上一节点内容，所以最朴素的方法就是先用数组记下来所有节点值，然后再逆序建个新链表。或者再建一条链，遍历当前链不断给新链插入头节点。但是这样都会增加空间消耗。

&emsp;&emsp;考虑上几道题的双指针，这道题难点就在于没办法知道上一个节点，那么在遍历时新建一个上一个节点就好了。先判断链表是否为空或者只有一个节点，是的话就直接返回；不是的话，设置当前节点为第二个节点，第一节点就是上一个节点 curNode = head.next，lastNode = head，lastNode.next = null。接下来遍历链表，如果当前节点有下一个节点，那就新建一个临时节点先保存 curNode.next，这个时候逆序处理，当前节点的下一节点应该是上一个节点 lastNode，之后上一个节点顺移为 curNode，curNode节点顺移为 临时节点。链表遍历结束后，curNode 的 next 设置为 lastNod。

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
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        ListNode curNode = head.next;
        ListNode lastNode = head;
        lastNode.next = null;
        while(curNode.next != null){
            ListNode tempNode = curNode.next;
            curNode.next = lastNode;
            lastNode = curNode;
            curNode = tempNode;
        }
        curNode.next = lastNode;
        return curNode;
    }
}
```

