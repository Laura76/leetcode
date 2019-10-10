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
- No.103 二叉树的锯齿形层次遍历 迭代
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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res=new LinkedList<>();
        if(root==null)return res;
        Queue<TreeNode> q=new LinkedList<>();
        q.add(root);
        int level=0;
        while(!q.isEmpty()){
            res.add(new ArrayList<>());
            int size=q.size();
            for(int i=0;i<size;i++){
                TreeNode  temp=q.remove();
                res.get(level).add(temp.val);
                if(temp.left!=null)q.add(temp.left);
                if(temp.right!=null)q.add(temp.right);
            }
            if(level%2==1)Collections.reverse(res.get(level));
            level++;
        }
        return res;
    }
}
```
- No.104 二叉树的最大深度 **迭代**
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
import javafx.util.Pair;
class Solution {
    public int maxDepth(TreeNode root) {
        if(root==null)return 0;
        Queue<Pair<TreeNode,Integer>> q=new LinkedList<>();
        q.add(new Pair(root,1));
        int depth=0;
        while(!q.isEmpty()){
            Pair<TreeNode,Integer> temp=q.remove();
            TreeNode node=temp.getKey();
            int curr_depth=temp.getValue();
            if(node!=null){
                depth=Math.max(depth,curr_depth);
                q.add(new Pair(node.left,curr_depth+1));
                q.add(new Pair(node.right,curr_depth+1));
            }
        }
        return depth;
    }
}
```
- No.105 从前序与中序遍历序列构造二叉树 **递归**
将数组的值和它对应的索引存在哈希表中，方便查询。
并且使用左右边界值的方式避免了数组的截取（我这样写希望一个月之后的我可以看懂）
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
    private int len;
    private HashMap<Integer,Integer> map=new HashMap<>();
    private int[] basicValue;
    private TreeNode buildTreeCore(int preleft,int preright,int inleft,int inright){
        if(preleft>preright||inleft>inright)return null;
        TreeNode root=new TreeNode(basicValue[preleft]);
        int temp=map.get(basicValue[preleft]);
        root.left=buildTreeCore(preleft+1,preleft+temp-inleft,inleft,temp-1);
        root.right=buildTreeCore(preleft+temp-inleft+1,preright,temp+1,inright);
        return root;
    }
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        this.len=preorder.length;
        //用哈希表将数组的值和它的索引做一个对应
        for(int i=0;i<len;i++){
            this.map.put(inorder[i],i);
        }
        this.basicValue=preorder;
        return buildTreeCore(0,len-1,0,len-1);
    }
}
```
