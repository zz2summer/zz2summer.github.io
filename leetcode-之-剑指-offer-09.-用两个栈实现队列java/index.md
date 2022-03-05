# LeetCode 之 剑指 Offer 09. 用两个栈实现队列（Java）


LeetCode 之 剑指 Offer 09. 用两个栈实现队列（Java），用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1。本文讲解实现思路和提供代码参考。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof)

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

 

示例 1：
```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```
示例 2：
```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```
提示：
```
1 <= values <= 10000
最多会对 appendTail、deleteHead 进行 10000 次调用
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 二、解题思路
首先，理清楚概念：
- 栈：先进后出
- 队列：先进先出

其次，从外部看，我们只需要保证3点即可：
- 数据存储仍然是按照既定顺序的
- 每次插入都是在尾部
- 每次删除都是在头部

最后，根据题目提示和要求，实现思路：
- 初始化两个栈，一个作为输入栈，每次插入都将数据放到顶部，另一个作为输出栈，直接将输入栈数据依次弹出然后添加到输出栈那么顺序就反过来了，每次删除直接弹出输出栈顶部
- 构造函数初始化
- 插入函数直接将数据添加到输入栈顶部
- 删除函数弹出输出栈顶部，但是需注意先确保将输入栈数据传到了输出栈


## 三、代码
```java
class CQueue {
    Stack<Integer> addStack;
    Stack<Integer> delStack;

    public CQueue() {
        addStack = new Stack<Integer>();
        delStack = new Stack<Integer>();
    }
    
    public void appendTail(int value) {
        addStack.add(value);
    }
    
    public int deleteHead() {
        // 输出栈若为空，则从输入栈先传数据过来
        if(delStack.isEmpty()){
            while(!addStack.isEmpty()){
                delStack.add(addStack.pop());
            }
        }
        if(delStack.isEmpty()){
            return -1;
        }else{
            return delStack.pop();
        }
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */
```

