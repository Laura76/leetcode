###### 以下题目按照难度排序，由易到难
---

- 257.二叉树的所有路径    
回溯（递归）
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
    List<String> res=new LinkedList<String>();
    private void binaryTreePathsCore(TreeNode node,Stack<String> pre){
        pre.push(String.valueOf(node.val));
        if(node.left==null&&node.right==null){
            StringBuilder builder=new StringBuilder();
            for(int i=0;i<pre.size();i++){
                if(i==pre.size()-1){
                    builder.append(pre.get(i));
                }else{
                    builder.append(pre.get(i)+"->");
                }
            }
            res.add(builder.toString());
            return;
        }
        if(node.left!=null){
            binaryTreePathsCore(node.left,pre);
            pre.pop();
        }
        if(node.right!=null){
            binaryTreePathsCore(node.right,pre);
            pre.pop();
        }
    }
    public List<String> binaryTreePaths(TreeNode root) {
        if(root==null)return res;
        binaryTreePathsCore(root,new Stack<String>());
        return res;
    }
}
```
- 437.路径总和3  
两层递归
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
    int res=0;
    private void pathSumCore(TreeNode node,int left,Stack<Integer> pre){
        if(node==null)return;
        if(left-node.val==0){
            //输出路径看一下
            res++;
        }
        if(node.left!=null){
            pre.push(node.val);
            pathSumCore(node.left,left-node.val,pre);
            pre.pop();
        }
        if(node.right!=null){
            pre.push(node.val);
            pathSumCore(node.right,left-node.val,pre);
            pre.pop();
        }
    }
    public int pathSum(TreeNode root, int sum) {
        if(root==null)return res;
        if(root.left==null&&root.right==null){
            return root.val==sum?++res:res;
        }
        pathSumCore(root,sum,new Stack<Integer>());
        if(root.left!=null){
            pathSum(root.left,sum);
        }
        if(root.right!=null){
            pathSum(root.right,sum);
        }
        return res;
    }
}
```
