- No.111 二叉树的最小深度 **递归**
```
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
    private int minDepthCore(TreeNode root){
        if(root==null)return 0;
        if(root.left==null&&root.right==null)return 1;
        if(root.left==null)return minDepthCore(root.right)+1;
        if(root.right==null)return minDepthCore(root.left)+1;
        return Math.min(minDepthCore(root.left),minDepthCore(root.right))+1;
    }
    public int minDepth(TreeNode root) {
        return minDepthCore(root);
    }
}
```
- No.112 路经总和 **回溯**  
回溯小能手就是我~
```
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
    private boolean hasPathSumCore(TreeNode root,int target){
        if(target==0&&root.left==null&&root.right==null)return true;
        if(root.left!=null){
            if(hasPathSumCore(root.left,target-root.left.val))return true;
        }
        if(root.right!=null){
            if(hasPathSumCore(root.right,target-root.right.val))return true;
        }
        return false;
    }
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root==null)return false;
        return hasPathSumCore(root,sum-root.val);
    }
}
```
