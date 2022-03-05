# LeetCode 之 剑指 Offer 10  II. 青蛙跳台阶问题（Java）


LeetCode 之 剑指 Offer 10- II. 青蛙跳台阶问题（Java），一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。利用函数思维转换为斐波那契数列问题，再采用递归或者记忆化数组解决。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof)

一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

示例 1：
```
输入：n = 2
输出：2
```
示例 2：
```
输入：n = 7
输出：21
```
示例 3：
```
输入：n = 0
输出：1
```
提示：
```
0 <= n <= 100
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 二、解题思路


&emsp;&emsp;这道题感觉其实还是挺巧妙的，如果没想通一下子也不好做。好吧，其实就是做题太少，自己太菜。
&emsp;&emsp;一开始我还想着按照正常思路这道题该怎么解，先假设全部为一跳完成，然后再有1个两跳，再2个两跳，最多n/2个两跳，将这些加起来就是最终的跳法。
然后代码不知从何下手。

&emsp;&emsp;对于这道题在最开始其实有个小提示，就是示例中的  f(0)=1 。
```
f(0)=1
f(1)=1
f(2)=2
……
```
&emsp;&emsp;f(2) 是怎么来的呢？要么f(1)跳一跳，要么f(0)跳两跳。So，f(2)=f(2-1)+f(2-2)……f(n)=f(n-1)+f(n-2)，到这里是不是就很眼熟了呢？这不就是斐波那契数列嘛！
&emsp;&emsp;[LeetCode 之 剑指 Offer 10- I. 斐波那契数列（Java）](https://summer2zz.blog.csdn.net/article/details/110423907)

&emsp;&emsp;对于算法题，如果不能理解题目，肯定就是先按照正常生活中的思路去找解决方式理解题目，然后再进一步转化为代码。但是，其实即便不能在生活中解决直接上代码思维也是可以的，本来程序就是为了解决生活中的不便之处。特别像这道题，利用函数推导思维可以很快想出来，但是从生活中入手就有些局限了。

&emsp;&emsp;另，题目给的示例还是要仔细看一下，像这道题那个 f(0)=1 就是在示例中给出的，一般人默认肯定是0。

## 三、代码
```java
class Solution {
    public int numWays(int n) {
        int constant = 1000000007;

        if(n==0){
            return 1;
        }
        if(n==1){
            return 1;
        }
        int[] nums = new int[n+1];
        nums[0] = 1;
        nums[1] = 1;
        for(int i=2; i<n+1; i++){
            nums[i] = (nums[i-1] + nums[i-2])%constant;
        }
        return nums[n];
    }
}
```

