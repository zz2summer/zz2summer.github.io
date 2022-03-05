# LeetCode 之 剑指 Offer 04. 二维数组中的查找（Java）


LeetCode 之 剑指 Offer 04. 二维数组中的查找（Java），在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。本文简要分析解题思路，提供暴力遍历和规律性删减法。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 04. 二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof)
在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

 

示例:

现有矩阵 matrix 如下：
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
给定 target = 5，返回 true。

给定 target = 20，返回 false。

 

限制：
```
0 <= n <= 1000

0 <= m <= 1000
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 二、解题思路

这道题的数据范围限制1000，倒也不影响遍历，但是既然数组是存在规律性的分布，那么肯定也就有更优的解法了。

解法1：遍历
暴力遍历每行每列，判断是否存在 target，反正也不会超时
O(n*m)

解法2：判断舍弃不必要的列
按照数组的规律，可以发现在当前行当我们从右往左遍历时，如果该数字大于 target，那么也就意味该列的数据都是大于 target 的，所以该列也就没有继续比较的必要了。
然后我们只需要遍历第一个小于 target 的列和所有行。
O(n*i)

解法3：对比删减行列法
在解法2的基础上，我们可以发现，如果当前行该列的数据小于 target 时，其实也就意味着该行可以不必比较了（我们从右往左遍历，所有目前的数据的左边的数据都是小于 target）
这样的话，我们可以选择从右上角出发进行查找，如果该数据小于target，则下一行，等于return，大于target，左一列
第一步：判断数组是否为空
第二步：右上角数据出发比对遍历循环
第三步：该数据 == target，return true
    该数据 > target，列--
    该数据 < target，行++
O(n+m)

## 三、代码
### 1. 遍历
```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if(matrix==null || matrix.length==0 || matrix[0].length==0){
            return false;
        }
        // int b=0;
        int n = matrix.length;
        int m = matrix[0].length;

        1.遍历 O(n*m)
         for(int i=0; i<n; i++){
             for(int j=0; j<m; j++){
                 if(matrix[i][j] == target){
                     return true;
                 }
             }
         }

        return false;


    }
}
```
### 2. 判断舍弃不必要的列
```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if(matrix==null || matrix.length==0 || matrix[0].length==0){
            return false;
        }
        // int b=0;
        int n = matrix.length;
        int m = matrix[0].length;

        //2.查找，舍弃不必要的列 O(m+n*b)
         for(int i=m-1; i>=0; i--){
             if(matrix[0][i]<target){
                 b = i;
                 break;
             }
             if(matrix[0][i] == target){
                 return true;
             }
         }
         for(int i=b; i>=0; i--){
             for(int j=0; j<n; j++){
                 if(matrix[j][i] == target){
                     return true;
                 }
             }
         }

        return false;

    }
}
```
### 3. 对比删减行列法
```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if(matrix==null || matrix.length==0 || matrix[0].length==0){
            return false;
        }
        // int b=0;
        int n = matrix.length;
        int m = matrix[0].length;

        //3.对比删减遍历查找 O(n+m)
        int row = 0;
        int col = m-1;
        while(row<n && col>=0){
            if(matrix[row][col] == target){
                return true;
            }
            if(matrix[row][col] > target){
                col--;
            }else{
                row++;
            }
        }

        return false;

    }
}
```

