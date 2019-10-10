- No.101 对称二叉树
用迭代还是勉强可以让我接受。我还是很讨厌笨蛋啰嗦的写法
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
    public boolean isSymmetric(TreeNode root) {
        Queue<TreeNode> queue=new LinkedList<TreeNode>();
        queue.add(root);
        queue.add(root);
        while(!queue.isEmpty()){
            TreeNode node1=queue.poll();
            TreeNode node2=queue.poll();
            if(node1==null&&node2==null)continue;
            if((node1==null)^(node2==null))return false;
            if(node1.val!=node2.val)return false;
            queue.add(node1.left);
            queue.add(node2.right);
            queue.add(node1.right);
            queue.add(node2.left);
        }
        return true;
    }
}
```
- No.102 二叉树的层次遍历 迭代
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res=new LinkedList<>();
        if(root==null)return res;
        Queue<TreeNode> queue=new LinkedList<TreeNode>();        
        queue.add(root);
        int level=0;
        while(!queue.isEmpty()){
            res.add(new ArrayList<Integer>());
            int size=queue.size();
            for(int i=0;i<size;i++){
                TreeNode temp=queue.remove();                
                res.get(level).add(temp.val);
                if(temp.left!=null)queue.add(temp.left);
                if(temp.right!=null)queue.add(temp.right);
            }
            level++;
        }
        return res;
    }
}
```
