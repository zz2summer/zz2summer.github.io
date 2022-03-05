# LeetCode 之 剑指 Offer 07. 重建二叉树（Java）


LeetCode 之 剑指 Offer 07. 重建二叉树（Java），输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。本文简单描述解题思路，如何重新划分前序遍历和中序遍历的二叉树根节点、左右子树，并提供实现代码。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 一、题目
[剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

例如，给出
```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
```
返回如下的二叉树：
```
    3
   / \
  9  20
    /  \
   15   7
```

限制：
```
0 <= 节点个数 <= 5000
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
## 二、解题思路

前序遍历：根节点、左子树、右子树
中序遍历：左子树、根节点、右子树

理解基本概念后，我们很容易看出，可以对其进行划分，得到根节点和左右子树，然后对左右子树再递归划分，就可以得到最终重建的二叉树。

- 对原始数组划分根节点、左右子树
- 判断是否生成左右子树，如果生成则调用递归函数传入左右子树的数据信息，包含前序数组中的开始下标、中序数组中的开始下标、树长度
- 在递归函数中则是不断对传入的左右子树进行三部分划分

## 三、代码
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        // 判断输入是否为空
        if(preorder.length == 0){
            return null;
        }
        TreeNode start = new TreeNode(preorder[0]);
        // 第一次划分左右子树
        for(int i=0; i<inorder.length; i++){
            if(inorder[i] == preorder[0]){
                //判断是否创建左子树，即前序和中序的第一个数据是否相同
                if(i != 0){
                    start.left = bulidBranch(preorder, inorder, start.left, 1, 0, i);
                }
                // 判断是否创建右子树，即该根节点右侧是否还有数据
                if(i+1 < inorder.length){
                    start.right = bulidBranch(preorder, inorder, start.right, 1+i, i+1, inorder.length-i-1);
                }
                
            }
        }
        
        return start;
    }

    // preStart:前序开始的下标, inStart:中序开始的下标, n:本次子树的长度
    TreeNode bulidBranch(int[] preorder, int[] inorder, TreeNode root, int preStart, int inStart, int n){
        root = new TreeNode(preorder[preStart]);
        for(int i=inStart; i<inStart+n; i++){
            if(inorder[i] == preorder[preStart]){
                if(i != inStart){
                    root.left = bulidBranch(preorder, inorder, root.left, preStart+1, inStart, i-inStart);
                }
                if(i+1 < inStart+n){
                    root.right = bulidBranch(preorder, inorder, root.right, preStart+i-inStart+1, i+1, n-(i-inStart)-1);
                }
            }
        }
        return root;
    } 
}
```

