- 第九十六题 不同的二叉搜索树
我真的爱死了动态规划，从小问题开始到大问题。真是很符合我这种头脑简单的人了。
```
class Solution {
    public int numTrees(int n) {
        int[] G=new int[n+1];
        G[0]=1;
        G[1]=1;
        for(int i=2;i<=n;i++){
            for(int j=0;j<=i-1;j++){
                G[i]+=G[j]*G[i-1-j];
            }
        }
        return G[n];
    }
}
```
- 第九十七题 交错字符串 困难 最近心有点浮躁，请静下心来，如果真的不会的话，那就远离人群和表达吧。
- 第九十八题 验证二叉搜索树
我讨厌递归
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
    private boolean isValidBSTCore(TreeNode root,Integer lower,Integer upper){
        if(root==null)return true;
        if(upper!=null){
            if(root.val>=upper)return false;
        }
        if(lower!=null){
            if(root.val<=lower)return false;
        }
        if(!isValidBSTCore(root.left,lower,root.val))return false;
        if(!isValidBSTCore(root.right,root.val,upper))return false;
        return true;
    }
    public boolean isValidBST(TreeNode root) {
        return isValidBSTCore(root,null,null);
    }
}
```
- 第九十九题 恢复二叉搜索树 困难  
能不能让我离开二叉树
- 第一百题 相同的树 终于过了前一百题了
什么东西最恶心？递归加上二叉树
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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p==null&&q==null)return true;
        if(p==null||q==null)return false;
        if(p.val!=q.val)return false;
        return isSameTree(p.left,q.left)&&isSameTree(p.right,q.right);
    }
}
```