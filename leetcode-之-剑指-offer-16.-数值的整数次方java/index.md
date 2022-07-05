# LeetCode 之 剑指 Offer 16. 数值的整数次方（Java）


剑指 Offer 16. 数值的整数次方实现 pow(x, n) ，即计算 x 的 n 次幂函数（即，xn）。不得使用库函数，同时不需要考虑大数问题。

<!--more-->

> 版权声明：本文为博主 [渣渣的夏天](https://zz2summer.github.io/) 的原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目

[剑指 Offer 16. 数值的整数次方](https://leetcode.cn/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

实现 pow(x, n) ，即计算 x 的 n 次幂函数（即，x^n^）。不得使用库函数，同时不需要考虑大数问题。

示例 1：

```bash
输入：x = 2.00000, n = 10
输出：1024.00000
```

示例 2：

```bash
输入：x = 2.10000, n = 3
输出：9.26100
```

示例 3：

```bash
输入：x = 2.00000, n = -2
输出：0.25000
解释：2^-2 = (1/2)^2 = 1/4 = 0.25
```


提示：

```bash
-100.0 < x < 100.0
-2^31^ <= n <= 2^31^-1
-10^4^ <= x^n^ <= 10^4^
```

来源：力扣（LeetCode）

链接：https://leetcode.cn/problems/shu-zhi-de-zheng-shu-ci-fang-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 二、解题思路

&emsp;&emsp;首先朴素的菜鸟方法，正数用 for 循环累乘 n 个 x，负数则先将 x 取倒数再将 n 取绝对值，考虑特殊情况 x=0。然后不出意外的话就是超时了。

### 1.递归

&emsp;&emsp;观察 x → x^2^ → x^4^ → x^16^ → x^32^ → x^64^ ，所以其实计算 x^64^ 时很多地方没必要再次逐个计算了。首先对于负数就是计算 x^-n^ 的倒数。正数就是不断计算 x^n/2^ ，如果 n 为奇数还需要再乘以 x。

### 2.迭代

&emsp;&emsp;又是数学知识，首先整数的二进制拆分为：n = 2^i0^ + 2^i1^ + …… + 2^ik^，那么 x^n^ = x^m0^ * x^m1^ * …… * x^mk^ ，其中 mk = 2^ik^ 。如果 x 二进制的第 k 位为 1 ，则需要纳入贡献。

注：本题计算方法又称快速幂方法。

## 三、代码

### 1.递归

```java
class Solution {
    public double myPow(double x, int n) {
        long N = n;
        return N >= 0 ? quickMul(x, N) : 1/quickMul(x, -N);
    }

    public double quickMul(double x, long N){
        if(N == 0){
            return 1.0;
        }
        double y = quickMul(x, N/2);
        return N%2==0 ? y*y : y*y*x;
    }
}
```

### 2.迭代

```java
class Solution {
    public double myPow(double x, int n) {
        long N = n;
        return N >= 0 ? quickMul(x, N) : 1/quickMul(x, -N);
    }

    public double quickMul(double x, long N){
        double ans = 1.0;
        // 记录每个项
        double x_con = x;
        while(N > 0){
            // 最后一位为1，纳入贡献
            if(N % 2 == 1){
                ans *= x_con;
            }
            x_con *= x_con;
            // 不断右移
            N /= 2;
        }
        return ans;
    }
}
```

