# LeetCode 之 剑指 Offer 17. 打印从1到最大的n位数（Java）


[剑指 Offer 17. 打印从1到最大的n位数](https://leetcode.cn/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)，输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

<!--more-->

> 版权声明：本文为博主 [渣渣的夏天](https://zz2summer.github.io/) 的原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 17. 打印从1到最大的n位数](https://leetcode.cn/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

示例 1:

```bash
输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]
```


说明：

- 用返回一个整数列表来代替打印
- n 为正整数

来源：力扣（LeetCode）

链接：https://leetcode.cn/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


## 二、解题思路

&emsp;&emsp;对于力扣上这题直接返回的是 int 数组，也就是没有考虑 n 位数可能超过给定的数值类型范围，所以思路很简单，直接获取 10^n-1 为最大值，然后 for 循环遍历填充数组即可，具体解法见【3.1 不考虑大数】。

&emsp;&emsp;大数的话一般考虑用字符串代表数字，这样相当于实现字符串的数字加法。

## 三、代码

### 3.1 不考虑大数

```java
class Solution {
    public int[] printNumbers(int n) {
        int m = 1;
        while(n>0){
            m *= 10;
            n--;
        }
        int[] ans = new int[m-1];
        for(int i=1; i<m; i++){
            ans[i-1] = i;
        }
        return ans;
    }
}
```

### 3.2 考虑大数

```java
class Solution {
    public int[] printNumbers(int n) {
        // 2.big data
        int m = 1;
        while(n>0){
            m *= 10;
            n--;
        }

        String[] ansStr = new String[m-1];
        ansStr[0] = "1";
        int cur = 1;
        while(cur < m-1){
            ansStr[cur] = strAddOne(ansStr[cur-1]);
            cur++;
        }
        
        // convert int
        int[] ans = new int[m-1];
        for(int i=0; i<m-1; i++){
            ans[i] = Integer.valueOf(ansStr[i]); 
        }
        return ans;
    }

    public String strAddOne(String ansStr){
        int n = ansStr.length();
        char[] ch = ansStr.toCharArray();
        int m = n-1;
        while(m >= 0 && ch[m]-'0' == 9){
            ch[m] = '0';
            m--;
        }
        if(m<0){
            return "1" + new String(ch);
        }else{
            ch[m] = (char)(ch[m]-'0'+1+'0');
        }
        return new String(ch);
    }
}
```

