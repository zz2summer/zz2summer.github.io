# LeetCode 之 剑指 Offer 06. 从尾到头打印链表（Java）


LeetCode 之 剑指 Offer 06. 从尾到头打印链表（Java），输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。本文主要分析解题思路并提供三种解法，分别是——1. "栈" + Stack，2. "栈" + ArrayList，3. 递归 + ArrayList。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

示例 1：
```
输入：head = [1,3,2]
输出：[2,3,1]
```

限制：
```
0 <= 链表长度 <= 10000
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
## 二、解题思路
本题两个难点：
1. 单向链表无法随机访问数据，即无法直接从后获取数据
2. 返回数组长度不定

单向链表逆序输出，那么也就是前面的最后输出，正好是栈的思想——先进后出。

然后单向链表的遍历时不可避免的，那么我们可不可以在遍历过程直接先从后往前输出呢？那就是递归。

所以本题两种解决思路:

### 栈

我们使用栈本质上是因为需要先获取再逆序保存，那么其实也有两种解法：
1. 直接使用Stack
    - 遍历链表读取数据到栈中
    - 根据栈的 size 创建返回的数组
    - 遍历数组获取栈中值，栈此时输出的就是逆向的链表数据
 ```
时间复杂度：O(N)，遍历单向链表读取，遍历数组保存
空间复杂度：O(N)，栈保存数据
 ```

2. 使用不定长数组ArrayList后逆序保存到输出结果
    - 遍历链表直接保存数据到ArrayList
    - 根据已经得到的ArrayList长度创建返回数组
    - 遍历返回数组，从后读取ArrayList数据到返回数组中
 ```
时间复杂度：O(N)，遍历单向链表读取，遍历数组保存
空间复杂度：O(N)，ArrayList保存数据
 ```

### 递归
递归其实也需要利用一个数组来保存中间值，也只能是不定长数组ArrayList
- 利用递归函数得到逆序的数组，判断head是否为null，是则结束，不是则调用该函数继续递归
- 根据ArrayList长度创建返回数组
- 直接顺序保存ArrayList中的数据到返回数组中
 ```
时间复杂度：O(N)，遍历单向链表读取，遍历数组保存
空间复杂度：O(N)，ArrayList保存数据
 ```
## 三、代码
### 1. "栈" + Stack
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
    public int[] reversePrint(ListNode head) {
		//1.1 直接调用Stack
        Stack<ListNode> stack = new Stack<ListNode>();

        //链表数据入栈
        ListNode temp = head;
        while(temp != null){
            stack.push(temp);
            temp = temp.next;
        }

        //栈数据存到数组
        int size = stack.size();
        int[] arr = new int[size];
        for(int i=0; i<size; i++){
            arr[i] = stack.pop().val;
        }
        
        return arr;
    }
}
```
### 2. "栈" + ArrayList
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
    public int[] reversePrint(ListNode head) {
        //1.2 借用ArrayList实现栈
        ArrayList<Integer> temp = new ArrayList<Integer>();
        while(head != null){
            temp.add(head.val);
            head = head.next;
        }
        int arrLen = temp.size();
        int[] arr = new int[arrLen];
        for(int i=0; i<arrLen; i++){
            arr[i] = temp.get(arrLen-1-i);
        }
        return arr;
    }
}
```
### 3. 递归 + ArrayList
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution{
    ArrayList<Integer> temp = new ArrayList<Integer>();
    public int[] reversePrint(ListNode head){
        m(head);
        int[] arr = new int[temp.size()];
        for(int i=0; i<arr.length; i++){
            arr[i] = temp.get(i);
        }
        return arr;
    }

    void m(ListNode head){
        if(head == null){
            return;
        }
        m(head.next);
        temp.add(head.val);
    }
}
```

