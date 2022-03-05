# LeetCode 之 剑指 Offer 05. 替换空格（Java）


LeetCode 之 剑指 Offer 05. 替换空格（Java），请实现一个函数，把字符串 s 中的每个空格替换成"%20"。解题思路：创建一个返回字符串，然后遍历原字符串利用字符串函数拼接或者替换后拼接即可。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof)

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

 

示例 1：
```
输入：s = "We are happy."
输出："We%20are%20happy."
```

限制：
```
0 <= s 的长度 <= 10000
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 二、解题思路
创建一个返回字符串，然后遍历原字符串利用字符串函数拼接或者替换后拼接即可。

## 三、代码
```java
class Solution {
    public String replaceSpace(String s) {
        // 遍历替换
        String s2 = "";
        for(int i=0; i<s.length(); i++){
            if(s.charAt(i)==' '){
                s2 = s2.concat("%20");
            }else{
                s2 = s2.concat(String.valueOf(s.charAt(i)));
            }
        }
        return s2;
    }
}
```

