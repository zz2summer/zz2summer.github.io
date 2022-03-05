# LeetCode 之 剑指 Offer 10  I. 斐波那契数列（Java）


LeetCode 之 剑指 Offer 10- I. 斐波那契数列（Java），写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项。最直接的方法当然是用递归，但是递归耗时过多，不适用，本文结合相关题解提供一个记忆化数组的方法进行解决。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof)

写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项。斐波那契数列的定义如下：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

 

示例 1：
```
输入：n = 2
输出：1
```
示例 2：
```
输入：n = 5
输出：5
```

提示：
```
0 <= n <= 100
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 二、解题思路

&emsp;&emsp;首先想到的自然是递归遍历法，但是这样的话O(n)就是2^n，最多到41可以行，之后就超时了。
&emsp;&emsp;后面看看解答，其实递归遍历就是从后向前不断计算，然后很多个数据都会重复计算，这样的话也就导致数据越大就越容易超时了。
&emsp;&emsp;所以，其实一想，既然反正都是要一个个计算，何不一开始就逐个计算下去呢？直到计算到n的前一个，然后就可以直接运用公式计算F(N)了。这样的O(N)也才N。

## 三、代码
```java
class Solution {
    public int fib(int N) {
        // 记忆化
        if(N<=1){
            return N;
        }else{
            int[] nums = new int[N];
            nums[0] = 0;
            nums[1] = 1;
            for(int i=2; i<N; i++){
                nums[i] = nums[i-1] + nums[i-2];
            }
            return nums[N-1]+nums[N-2];
        }



        // 递归遍历，O(N) 2^n
        // if(N<=1){
        //     return N;
        // }else{
        //     return fib(N-1) + fib(N-2);
        // }
    }
}
```

