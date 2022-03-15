# LeetCode 之 剑指 Offer 14  II. 剪绳子 II （Java） 


LeetCode 之 剑指 Offer 14- II. 剪绳子 II （Java） ，给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 `k[0],k[1]...k[m - 1] `。请问 `k[0]*k[1]*...*k[m - 1]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 14- II. 剪绳子 II](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/)

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 `k[0],k[1]...k[m - 1] `。请问 `k[0]*k[1]*...*k[m - 1]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

答案需要取模 `1e9+7（1000000007）`，如计算初始结果为：`1000000008`，请返回 1。

示例 1：

```bash
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```

示例 2:

```bash
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

提示：

```bash
2 <= n <= 1000
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/jian-sheng-zi-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 二、解题思路

&emsp;&emsp;这道题主要是将 n 的范围扩大了，然后结果可能越界需要取模，进而代码方面会有些改动。

### 1.动态规划

&emsp;&emsp;方法是一样的，但是需要用到大数操作——`java.math.BigInteger`，初始化、相乘、取最大值和最后的取余这四处地方需要修改。（此时的 Math.max 已不适用与取模后做比较了）

### 2.贪婪算法

&emsp;&emsp;思路同原题，主要是在求 3^n^ 时要不断的取余防止溢出。

## 三、代码

### 3.1 动态规划

```java
import java.math.BigInteger;
class Solution {
    public int cuttingRope(int n) {
        // 3.1 DP
        if(n<2){
            return 0;
        }
        if(n==2){
            return 1;
        }
        if(n==3){
            return 2;
        }
        // n=2,3 具有特殊性，单独时必须至少剪一刀，所以f(2)=1,f(3)=2，但是放到剪的两侧时其实最大为2,3，所以动态公式从 4 开始，f(n)=Max(f(i)*f(n-i)) (n>3,i<=n/2)
        BigInteger[] m = new BigInteger[n+1];
        for(int i=0; i<n+1; i++){
            m[i] = BigInteger.valueOf(1);
        }
        m[2] = BigInteger.valueOf(2);
        m[3] = BigInteger.valueOf(3);
        for(int i=4; i<n+1; i++){
            for(int j=1; j<=i/2; j++){
                // m[i] 缓存遍历 j 时前面所有的剪法的最大值，直到最后为所有分法的最大值，Math.max已不适用
                m[i] = m[i].max(m[j].multiply(m[i-j]));
            }
        }
        return m[n].mod(BigInteger.valueOf(1000000007)).intValue();
    }
}
```

### 3.2 贪婪算法

```java
class Solution {
    public int cuttingRope(int n) {
        // 3.2 贪婪
        if(n<2){
            return 0;
        }
        if(n==2){
            return 1;
        }
        if(n==3){
            return 2;
        }
        long p = 1000000007;
        long res = 1;
        while(n>4){
            res = res * 3 % p;
            n -= 3;
        }
        return (int)(res * n % p);
    }
}
```

