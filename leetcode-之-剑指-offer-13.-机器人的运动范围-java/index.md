# LeetCode 之 剑指 Offer 13. 机器人的运动范围 （Java）


LeetCode 之 剑指 Offer 13. 机器人的运动范围（Java），地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

示例 1：

```bash
输入：m = 2, n = 3, k = 1
输出：3
```


示例 2：

```bash
输入：m = 3, n = 1, k = 0
输出：1
```

提示：

```bash
1 <= n,m <= 100
0 <= k <= 20
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


## 二、解题思路

&emsp;&emsp;本题与上一题的矩阵路径很相似，感觉还简单些，就是起点是 [0, 0]，判断当前点能够进入然后再遍历四周的点，每次移动到四周点时再将该点作为起点即可。

&emsp;&emsp;三个细节：

&emsp;&emsp;一是判断进入函数，根据题目提示的 m, n 范围可以直接当做三位数取位数和计算 check 能够进入（不确定位数的则可以用 while 不断遍历截取）；

&emsp;&emsp;二是对于每次点向四周移动时应该有一个 visited 二维数组记录是否来过，如果来过就不再过去了；

&emsp;&emsp;三是计算总格子时是当前格子加上四周能够继续进入的格子数，所以在进入当前点时应该 ans++ ，然后再加上四周新进入的点。

## 三、代码
```java
class Solution {
    public int movingCount(int m, int n, int k) {
        int ans = 0;
        int[][] visited = new int[m][n];

        ans += move(0, 0, k, visited, m, n);

        return ans;
    }

    public boolean check(int i, int j, int k){
        if(i%10 + i/10%10 + i/100 + j%10 + j/10%10 + j/100 <= k){
            return true;
        }
        return false;
    }
    
    public int move(int i, int j, int k, int[][] visited, int m, int n){
        int ans = 0;
        if(check(i,j, k)){
            visited[i][j]=1;
            ans++;
            int[][] directions = { {0,1}, {0,-1}, {-1,0}, {1,0}};
            for(int[] dir : directions){
                int newi = i+dir[0];
                int newj = j+dir[1];
                if(newi>=0&&newi<m && newj>=0&&newj<n && visited[newi][newj]==0){
                    ans += move(newi, newj, k, visited, m, n);
                }
            }  
        }
        return ans;
    }
}
```

