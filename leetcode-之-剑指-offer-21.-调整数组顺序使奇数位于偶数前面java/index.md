# LeetCode 之 剑指 Offer 21. 调整数组顺序使奇数位于偶数前面（Java）


[剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](https://leetcode.cn/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)，输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数在数组的前半部分，所有偶数在数组的后半部分。

<!--more-->

> 版权声明：本文为博主 [渣渣的夏天](https://zz2summer.github.io/) 的原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](https://leetcode.cn/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数在数组的前半部分，所有偶数在数组的后半部分。

示例：

```bash
输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。
```


提示：

1. 0 <= nums.length <= 50000
2. 0 <= nums[i] <= 10000

来源：力扣（LeetCode）

链接：https://leetcode.cn/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


## 二、解题思路

&emsp;&emsp;最直接的思路遍历，遇到偶数时先把后面的数据往前移，把该偶数再放最后一位，时间复杂度 O(n^2)。

&emsp;&emsp;比较典型的就是双指针，同时从前后遍历数组（遍历过程保证 start < end），前面遇到偶数时停下，后面遇到奇数停下，然后交换，再继续直接 start >= end。

## 三、代码
```java
class Solution {
    public int[] exchange(int[] nums) {
        int n = nums.length;
        int start = 0;
        int end = n-1;
        while(start<end){
            while(start < end && nums[start]%2!=0){
                start++;
            }
            while(start < end && nums[end]%2==0){
                end--;
            }
            if(start < end){
                int temp = nums[start];
                nums[start] = nums[end];
                nums[end] = temp;
            }
        }
        return nums;
    } 
}
```

