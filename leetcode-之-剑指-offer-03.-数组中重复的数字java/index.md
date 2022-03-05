# LeetCode 之 剑指 Offer 03. 数组中重复的数字（Java）


LeetCode 之 剑指 Offer 03. 数组中重复的数字（Java），在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。创建重复数组进行遍历判断。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 03. 数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof)

找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例 1：
```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```

限制：
```
2 <= n <= 100000
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
## 二、解题思路
此题比较巧妙，长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内，找出任意重复的一个数字，那么可以直接创建一个等长的数组，默认值均为0，然后遍历原数组中的值，先判断改以该值为下标的复制数组中的数据是否为0，如果是，则将其改为1，表示已经有数值了，等后面再次遇到该值为下标时，则复制数组的数据不再为1，表示重复了。

简单讲，将原始数组中的每个数值放到复制数组中的以该值为下标的位置处，并将该位置值改为1，表示有该数据，然后在后续遍历遇到该数据发现是1则重复了。


## 三、代码
```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        int n = nums.length;
        int[] a = new int[n];
        int result = 0;
        for(int i=0; i<n; i++){
            if(a[nums[i]] == 0){
                a[nums[i]] = 1;
            }else{
                result = nums[i];
                break;
            }
        }
        return result;
    }
}
```
