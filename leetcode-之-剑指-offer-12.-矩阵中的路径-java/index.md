# LeetCode 之 剑指 Offer 12. 矩阵中的路径 （Java）


LeetCode 之 剑指 Offer 12. 矩阵中的路径（Java），给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)

给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

例如，在下面的 3×4 的矩阵中包含单词 "ABCCED"（单词中的字母已标出）。

![image-20220306135702968](/LeetCode/image-20220306135702968.png)

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


## 二、解题思路

&emsp;&emsp;对于二维数组的找路径问题，一般的建议是考虑使用回溯。遍历每个点，每次以当前点为起点，判断后续是否有继续的可能性，只需要考虑一次以当前点为起点的后续可能性并对每种可能性进行处理即可。

&emsp;&emsp;以本题为例，首先遍历二维数组中的每个点，两个 for 循环即可，之后对于每个点调用一个 check 的方法，判断以该点以起点后续有没有机会继续完成要求，也就是继续遍历完题目给定的 word ，如果有可能返回 true。调用后将

&emsp;&emsp;在 check 函数中，对于每个点，有四种选择的可能性——上下左右，所以会有一个 for 循环遍历四个方向，对于每个方向有三种可能性：

1. 当前点不是当前需要满足的字符，直接返回 false；

2. 当前点是当前需要满足的字符，并且该字符已经是给定 word 的最后一个字符，直接返回 true；

3. 当前点是当前需要满足的字符，但是不是最后一个。此时将该点标记为已访问（防止接下来按四个方向遍历时又访问已经标记过的点），继续遍历上下左右四个方向，对于每个方向仍然调用 check 方法判断时候有可能继续完成剩余字符串的路径查找。

   注意，不管此次是否找到结果，最后返回时都应当将 visited 标记为 false 表示该点未访问，因为每次的遍历都是从二维数组当前点为初始起点考虑的，也就是每次所有的点都应当是全新未访问的。

## 三、代码
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int h = board.length, w = board[0].length;
        boolean[][] visited = new boolean[h][w];
        for(int i=0; i<h; i++){
            for(int j=0; j<w; j++){
                boolean flag = check(board, visited, i, j, word, 0);
                if(flag){
                    return true;
                }
            }
        }
        return false;
    }

    public boolean check(char[][] board, boolean[][] visited, int i, int j, String s, int k){
        if(board[i][j] != s.charAt(k)){
            return false;
        }else if(k==s.length()-1){
            return true;
        }
        visited[i][j] = true;
        int[][] dirctions = { {0,1}, {0,-1},{1,0},{-1,0}};
        boolean result = false;
        for(int[] dir : dirctions){
            int newi = i+dir[0], newj = j+dir[1];
            if(newi>=0&&newi<board.length && newj>=0&&newj<board[0].length){
                if(!visited[newi][newj]){
                    boolean flag = check(board, visited, newi, newj, s, k+1);
                    if(flag){
                        result = true;
                        break;
                    }
                }
            }
        }
        visited[i][j] = false;
        return result;
    }
}
```

