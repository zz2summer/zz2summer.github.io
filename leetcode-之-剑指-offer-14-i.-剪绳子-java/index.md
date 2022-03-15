# LeetCode 之 剑指 Offer 14  I. 剪绳子 （Java） 


LeetCode 之 剑指 Offer 14- I. 剪绳子 （Java） ，给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 `k[0],k[1]...k[m-1] `。请问 `k[0]*k[1]*...*k[m-1]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 14- I. 剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 `k[0],k[1]...k[m-1] `。请问 `k[0]*k[1]*...*k[m-1]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

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
2 <= n <= 58
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/jian-sheng-zi-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 二、解题思路

### 1.动态规划

&emsp;&emsp;对于剪绳子，可以直接考虑将其剪为两段——`i,n-i` → `f(n) = Max(f(i)*f(n-i))`，其中 `i<=n/2 && i>3`，这个 `i>3` 就很巧妙。当 `i<2` 时 ，`f(i)=0`，然后 `f(2)=1,f(3)=2`，应为 `m>1`即最少要剪一刀。但是其实到了后面剪成两段时，如果出现 `i=2/3`，可以直接不剪，这样这段绳子在相乘时可以直接取 `2/3`。具体代码见解法3.1

&emsp;&emsp;网上还有种解法是说将绳子先剪一段 i ，然后剩下的 n-i 可以选择剪或者不剪，这样动规公式就是 `f(n)=Max(i*(n-i), i*m[n-i])`。但是其实细想至少按照动规思路来说，这个公式肯定是不对的。因为右侧可以剪或者不剪，那左侧自然也可以剪或者不剪，即动规应该是 `f(n)=Max(i*(n-i), i*m[n-i], m[i]*(n-i), m[i]*m[n-i])`。当然，那么做答案是对的，具体代码见解法3.2

### 2.贪婪算法

&emsp;&emsp;利用贪婪算法得在数学上证明成立，一般感觉不好想到。

&emsp;&emsp;本题中是说在 `n>4` 时，先尽可能剪成 3 最后得到的累乘最大。这时剩下的长度可能为 `0,1,2`，如果为 0，这时正好不用管；如果为 1，这时可以从前面取一个 3，组成 2\*2 更合适（3\*1 < 2\*2）；如果最后为 2，那也不用管。所以最终的答案就是 2 和 3 分别剪了多少段。

## 三、代码

### 3.1 动态规划1

```java
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
        int[] m = new int[n+1];
        m[1] = 1;
        m[2] = 2;
        m[3] = 3;
        for(int i=4; i<n+1; i++){
            for(int j=1; j<=i/2; j++){
                // m[i] 缓存遍历 j 时前面所有的剪法的最大值，直到最后为所有分法的最大值
                m[i] = Math.max(m[j]*m[i-j], m[i]);
            }
        }
        return m[n];
    }
}
```

### 3.2 动态规划2

```java
class Solution {
    public int cuttingRope(int n) {
        // 3.2 DP
        if(n<2){
            return 0;
        }
        if(n==2){
            return 1;
        }
        int[] m = new int[n+1];
        m[1] = 1;
        m[2] = 1;
        for(int i=3; i<n+1; i++){
            for(int j=1; j<=i/2; j++){
                m[i] = Math.max(Math.max(j*(i-j), j*m[i-j]), m[i]);
            }
        }

        return m[n];
    }
}
```

### 3.3 贪婪算法

```java
class Solution {
    public int cuttingRope(int n) {
        // 3.3 贪婪
        if(n<2){
            return 0;
        }
        if(n==2){
            return 1;
        }
        if(n==3){
            return 2;
        }
        int t3 = n/3;
        if(n-t3*3==1){
            t3--;
        }
        int t2 = (n-t3*3)/2;
        return (int)Math.pow(3,t3)*(int)Math.pow(2,t2);
    }
}
```

