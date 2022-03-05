# LeetCode 之 剑指 Offer 11. 旋转数组的最小数字（Java）


剑指 Offer 11. 旋转数组的最小数字，把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。给你一个可能存在 重复 元素值的数组 numbers ，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一次旋转，该数组的最小值为1。  

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
 [剑指 Offer 11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。

给你一个可能存在 重复 元素值的数组 numbers ，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一次旋转，该数组的最小值为1。  

示例 1：

```bash
输入：[3,4,5,1,2]
输出：1
```

示例 2：

```bash
输入：[2,2,2,0,1]
输出：0
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


## 二、解题思路

&emsp;&emsp;对于题目中提到的升序旋转数组其实看看例子就可以发现，每个最小的数字都是转折点。如果旋转个数为 0，那么第一个数字就是最小的。

&emsp;&emsp;所以直接考虑初始化最小数字为第一个，之后遍历数组，如果遇到比第一个数字更小的数字那一定是转折点，也是整个数组的最小值。

## 三、代码
```java
class Solution {
    public int minArray(int[] numbers) {
        int n = numbers.length;
        int nMin = numbers[0];
        for(int i=1;i<n;i++){
            if(numbers[i]<nMin){
                return numbers[i];
            }
        }
        return nMin;
    }
}
```

