- No.106 从中序与后序遍历序列构造二叉树 **递归**
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
    private int[] basicValue;
    private HashMap<Integer,Integer> map=new HashMap<>();
    private TreeNode buildTreeCore(int inleft,int inright,int postleft,int postright){
        if(inleft>inright||postleft>postright)return null;
        int temp=map.get(basicValue[postright]);
        TreeNode root=new TreeNode(basicValue[postright]);
        root.left=buildTreeCore(inleft,temp-1,postleft,postleft+temp-inleft-1);
        root.right=buildTreeCore(temp+1,inright,postleft+temp-inleft,postright-1);
        return root;
    }
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        int len=inorder.length;
        for(int i=0;i<len;i++){
            this.map.put(inorder[i],i);
        }
        this.basicValue=postorder;
        return buildTreeCore(0,len-1,0,len-1);
    }
}
```
- No.107 二叉树的层次遍历Ⅱ **迭代**
因为要从底层向首层输出，所以每次添加从list的开头添加。
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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res=new LinkedList<>();
        if(root==null)return res;
        Queue<TreeNode> q=new LinkedList<>();
        q.add(root);
        int level=0;
        while(!q.isEmpty()){
            LinkedList<Integer> nodetree=new LinkedList<>();
            int size=q.size();
            for(int i=0;i<size;i++){
                TreeNode temp=q.remove();
                nodetree.add(temp.val);
                if(temp.left!=null)q.add(temp.left);
                if(temp.right!=null)q.add(temp.right);
            }
            res.add(0,nodetree);
            level++;
        }
        return res;
    }
}
```
- No.108 将有序数组转换为二叉搜索树 **递归** **二分**  
我要死了,公主什么时候能打败递归。
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
    private TreeNode sortedArrayToBSTCore(int[] nums,int start,int end){
        if(start>end)return null;
        int mid=start+((end-start)>>1);
        TreeNode root=new TreeNode(nums[mid]);
        root.left=sortedArrayToBSTCore(nums,start,mid-1);
        root.right=sortedArrayToBSTCore(nums,mid+1,end);
        return root;
    }
    public TreeNode sortedArrayToBST(int[] nums) {
        return sortedArrayToBSTCore(nums,0,nums.length-1);
    }
}
```
- No.109 有序链表转换二叉搜索树 **递归**
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
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
    private TreeNode sortedListToBSTCore(List<Integer> data,int start,int end){
        if(start>end)return null;
        int mid=start+((end-start)>>1);
        TreeNode root=new TreeNode(data.get(mid));
        root.left=sortedListToBSTCore(data,start,mid-1);
        root.right=sortedListToBSTCore(data,mid+1,end);
        return root;
    }
    public TreeNode sortedListToBST(ListNode head) {
        List<Integer> data=new LinkedList<>();
        while(head!=null){
            data.add(head.val);
            head=head.next;
        }
        return sortedListToBSTCore(data,0,data.size()-1);
    }
}
```
- No.110 平衡二叉树 **递归**
公主好像有点懂递归了，以前都是从顶部往底部回想验证递归的过程，凭我垃圾的脑容量并不能回想成功，所以代码就改不了。
但是我发现从底部往顶部，即从递归结束往前回想验证的话，我可以完整的回想出递归的过程。所以还是从小问题想到大问题，和我学习动态规划是一样的。
WTM大二教的东西现在才领悟！！我的大学是怎么过的！
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
    private int isBalancedCore(TreeNode root){
        if(root==null)return 0;
        if(root.left==null&&root.right==null)return 1;
        int left=isBalancedCore(root.left);
        if(left==-1)return -1;
        int right=isBalancedCore(root.right);
        if(right==-1)return -1;
        if(Math.abs(left-right)>=2)return -1;
        return Math.max(left,right)+1;

    }
    public boolean isBalanced(TreeNode root) {
        return isBalancedCore(root)!=-1;
    }
}
```
