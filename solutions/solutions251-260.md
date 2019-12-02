- No.251-256 **氪金**
- No.257 二叉树的所有路径 **dfs**
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
    private void dfs(TreeNode root,Stack<String> stack){
        stack.push(String.valueOf(root.val));
        if(root.left==null&&root.right==null){  
            StringBuilder builder=new StringBuilder();
            for(String str:stack)builder.append(str+"->");
            int len=builder.toString().length();                     
            res.add(builder.toString().substring(0,len-2));
        }
        if(root.left!=null){
            dfs(root.left,stack);
            stack.pop();
        }
        if(root.right!=null){
            dfs(root.right,stack);
            stack.pop();
        }
    }
    public List<String> binaryTreePaths(TreeNode root) {
        if(root==null)return res;
        dfs(root,new Stack<String>());
        return res;
    }
}
```
- No.258 各位相加 **执行效率很低，待改善**
```
class Solution {
    public int addDigits(int num) {
        String temp=String.valueOf(num);
        while(temp.length()!=1){
            int sum=0;
            for(int i=0;i<temp.length();i++){
                sum+=(temp.charAt(i)-'0');
            }
            temp=String.valueOf(sum);
        }
        return Integer.valueOf(temp);
    }
}
```
- No.259 **氪金**
- No.260 只出现一次的数字 III
```
class Solution {
    public int[] singleNumber(int[] nums) {
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        int[] res=new int[2];int click=0;
        for(int i:nums){
            map.put(i,map.getOrDefault(i,0)+1);
        }
        Iterator<Map.Entry<Integer, Integer>> entries = map.entrySet().iterator();
        while(entries.hasNext()){
            Map.Entry<Integer, Integer> entry = entries.next();
            if(entry.getValue()==1)res[click++]=entry.getKey();
        }
        return res;
    }
}
```
