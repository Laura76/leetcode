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
- No.113 路径总和Ⅱ  **回溯**  
二叉树的回溯就是把循环改成了左右子树两种情况循环。
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
    private List<List<Integer>> res=new LinkedList<>();
    private void pathSumCore(TreeNode root,int target,Stack<Integer> pre){
        if(target==0&&root.left==null&&root.right==null){
            res.add(new LinkedList<>(pre));
            return;
        }
        if(root.left!=null){
            pre.push(root.left.val);
            pathSumCore(root.left,target-root.left.val,pre);
            pre.pop();
        }
        if(root.right!=null){
            pre.push(root.right.val);
            pathSumCore(root.right,target-root.right.val,pre);
            pre.pop();
        }
    }
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        if(root==null)return res;
        Stack<Integer> stack=new Stack<>();
        stack.push(root.val);
        pathSumCore(root,sum-root.val,stack);
        return res;
    }
}
```
- No.114 二叉树展开为链表   
为什么这么浮躁呢？哎哎哎
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
    public void flatten(TreeNode root) {
        TreeNode node=root;
        while(node!=null){
            if(node.left==null){
                node=node.right;
                continue;
            }else{
                TreeNode temp=node.left;
                while(temp.right!=null){
                    temp=temp.right;
                }
                temp.right=node.right;
                node.right=node.left;
                node.left=null;
                node=node.right;
            }
        }
    }
}
```