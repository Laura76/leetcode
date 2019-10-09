- 第九十一题 解码方法
使用动态规划的方法，但是有很多的小细节导致我提交了很多次。但是毕竟是第一次使用动态规划成功嘿嘿～今天的外教依旧很尬呃呃呃呃
```
class Solution {
    public int numDecodings(String s) {
        if(s.startsWith("0"))return 0;
        char[] nums=s.toCharArray();
        int len=nums.length;
        if(len==1&&Integer.valueOf(s)==0)return 0;
        int[] dp=new int[len+1];
        dp[0]=1;
        dp[1]=1;
        for(int i=2;i<=len;i++){
            dp[i]=nums[i-1]=='0'?0:dp[i-1];
            int temp=Integer.valueOf(s.substring(i-2,i));
            if(temp<=26&&temp>=10){
                dp[i]+=dp[i-2];
            }
        }
        return dp[len];
    }
}
```
- 第九十二题 暂时没有心情写，一直卡在这道题
- 第九十三题 复原IP地址
我讨厌回溯问题的各种烦人的细节
```
class Solution {
    private List<String> res=new LinkedList<String>();
    private void restoreIpAddressesCore(int depth,Stack<String> pre,String s){
        if(depth==4){
            if(s.length()==0){
                StringBuilder builder=new StringBuilder();
                for(String str:pre){
                    builder.append(str+".");
                }
                String temp=builder.toString();
                res.add(temp.substring(0,temp.length()-1));
            }
            return;
        }
        for(int i=0;i<s.length()&&Integer.valueOf(s.substring(0,i+1))<=255;i++){
            pre.push(s.substring(0,i+1));
            restoreIpAddressesCore(depth+1,pre,s.substring(i+1));
            pre.pop();
            if(s.charAt(0)=='0')break;
        }
    }
    public List<String> restoreIpAddresses(String s) {
        restoreIpAddressesCore(0,new Stack<String>(),s);
        return res;
    }
}
```
- 第九十四题 二叉树的中序遍历
注意有的时候markdown的代码片段显示有问题是因为代码片段中有空行的存在，智障？？？
所以这个中序遍历的while的终止条件是我抄答案的，我相信以后我肯定也想不起来。
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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res=new LinkedList<Integer>();
        Stack<TreeNode> stack=new Stack<TreeNode>();
        TreeNode curr=root;
        while(!stack.isEmpty()||curr!=null){
            while(curr!=null){
                stack.push(curr);
                curr=curr.left;
            }
            curr=stack.pop();
            res.add(curr.val);
            curr=curr.right;
        }
        return res;
    }
}
```
- 第九十五题 不同的二叉搜索树 II
我讨厌递归啊啊啊啊啊啊啊啊啊啊，谁能让我对递归开个窍吧！！！
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
    private List<TreeNode> generateTreesCore(int start,int end){
        List<TreeNode> res=new LinkedList<>();
        if(start>end){
            res.add(null);
            return res;
        }
        for(int i=start;i<=end;i++){
            List<TreeNode> left=generateTreesCore(start,i-1);
            List<TreeNode> right=generateTreesCore(i+1,end);
            for(TreeNode l:left){
                for(TreeNode r:right){
                    TreeNode root=new TreeNode(i);
                    root.left=l;
                    root.right=r;
                    res.add(root);
                }
            }
        }
        return res;
    }
    public List<TreeNode> generateTrees(int n) {
        if(n==0){
            return new ArrayList<TreeNode>();
        }
        return generateTreesCore(1,n);
    }
}
```
