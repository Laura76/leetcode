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
- 112.路径总和    
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
    boolean res=false;
    private void hasPathSumCore(TreeNode node,int left){
        if(res==true)return;
        if(node.left==null&&node.right==null){
            if(left-node.val==0){
                res=true;
                return;
            }else return;
        }
        if(node.left!=null){
            left-=node.val;
            hasPathSumCore(node.left,left);
            left+=node.val;
        }
        if(node.right!=null){
            left-=node.val;
            hasPathSumCore(node.right,left);
            left+=node.val;
        }
    }
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root==null)return false;
        hasPathSumCore(root,sum);
        return res;
    }
}
```
- 543.二叉树的直径  
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
    private int maxPath=0;
    private int diameterOfBinaryTreeCore(TreeNode node){
        if(node.left==null&&node.right==null){
            return 0;
        }
        int maxR=0;int maxL=0;
        if(node.right!=null){
            maxR=diameterOfBinaryTreeCore(node.right)+1;
        }
        if(node.left!=null){
            maxL=diameterOfBinaryTreeCore(node.left)+1;
        }
        maxPath=Math.max(maxR+maxL,maxPath);
        return Math.max(maxR,maxL);
    }
    public int diameterOfBinaryTree(TreeNode root) {
        if(root==null)return 0;
        diameterOfBinaryTreeCore(root);
        return maxPath;
    }
}
```
- 687.最长同值路径  
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
    private int res=0;
    private int longestUnivaluePathCore(TreeNode node){
        if(node.left==null&&node.right==null){
            return 0;
        }
        int maxR=0,maxL=0;
        if(node.right!=null){
            if(node.val!=node.right.val)
                longestUnivaluePathCore(node.right);
            else maxR=longestUnivaluePathCore(node.right)+1;

        }
        if(node.left!=null){
             if(node.val!=node.left.val)
                longestUnivaluePathCore(node.left);
            else maxL=longestUnivaluePathCore(node.left)+1;
        }
        res=Math.max(maxR+maxL,res);
        return Math.max(maxR,maxL);
    }
    public int longestUnivaluePath(TreeNode root) {
        if(root==null)return 0;
        longestUnivaluePathCore(root);
        return res;
    }
}
```
- 797.所有可能的路径  
回溯（递归）
```
class Solution {
    private List<List<Integer>> res=new LinkedList<>();
    private void allPathsSourceTargetCore(int start,Stack<Integer> pre,Set<Integer> set,int[][] graph){
        pre.push(start);
        if(start==0){
            LinkedList<Integer> temp=new LinkedList<Integer>();
            for(int i=pre.size()-1;i>=0;i--){
                temp.add(pre.get(i));
            }
            res.add(temp);
            return;
        }
        for(int i=0;i<graph.length;i++){
            if(!set.contains(i)){
                for(int j:graph[i]){
                    if(start==j){
                        Set<Integer> temp=new HashSet<Integer>();
                        for(int k:graph[i])temp.add(k);
                        allPathsSourceTargetCore(i,pre,temp,graph);
                        pre.pop();
                    }
                }
            }
        }
    }
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        if(graph.length==0)return res;
        Set<Integer> set=new HashSet<Integer>();
        for(int i:graph[graph.length-1])set.add(i);
        allPathsSourceTargetCore(graph.length-1,new Stack<Integer>(),set,graph);
        return res;
    }
}
```
- 64.最小路径和  
dp(自底向上的动态规划)
```
class Solution {
    public int minPathSum(int[][] grid) {
        int row=grid.length;
        if(row==0)return 0;
        int col=grid[0].length;
        for(int i=row-1;i>=0;i--){
            for(int j=col-1;j>=0;j--){
                if(i==row-1&&j!=col-1){
                    grid[i][j]+=grid[i][j+1];
                }else if(j==col-1&&i!=row-1){
                    grid[i][j]+=grid[i+1][j];
                }else if(j!=col-1&&i!=row-1){
                    grid[i][j]+=Math.min(grid[i][j+1],grid[i+1][j]);
                }
            }
        }
        return grid[0][0];
    }
}
```
- 120.三角形最小路径和  
dp(自底向上的动态规划)
```
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int row=triangle.size();
        if(row==0)return 0;
        int[] dp=new int[triangle.get(row-1).size()];
        for(int i=0;i<triangle.get(row-1).size();i++)dp[i]=triangle.get(row-1).get(i);
        for(int i=row-2;i>=0;i--){
            for(int j=0;j<triangle.get(i).size();j++){
                dp[j]=triangle.get(i).get(j)+Math.min(dp[j],dp[j+1] );
            }
        }
        return dp[0];
    }
}
```
- 666.路径和Ⅳ  
回溯（递归）
```
class Solution {
    private int res=0;
    private int[][] tree=new int[4][9];
    private void pathSumCore(int row,int col,Stack<Integer> pre){
        if(row==3||(tree[row+1][col*2-1]==-1&&tree[row+1][col*2]==-1)){
            pre.push(tree[row][col]);
            for(int i=0;i<pre.size();i++){
                res+=pre.get(i);
            }
            pre.pop();
            return;
        }
        if(tree[row+1][col*2-1]!=-1){
            pre.push(tree[row][col]);
            pathSumCore(row+1,col*2-1,pre);
            pre.pop();
        }
        if(tree[row+1][col*2]!=-1){
            pre.push(tree[row][col]);
            pathSumCore(row+1,col*2,pre);
            pre.pop();
        }
    }
    public int pathSum(int[] nums) {
        for(int i=0;i<tree.length;i++){
            for(int j=1;j<tree[0].length;j++){
                tree[i][j]=-1;
            }
        }
        for(int i:nums){
            int temp=i;
            tree[i/100-1][(i/=10)%10]=temp%10;
        }
        pathSumCore(0,1,new Stack<Integer>());
        return res;
    }
}
```
- 129.求根到叶子节点数字之和  
递归（回溯）
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
    private int res=0;
    private void sumNumbersCore(TreeNode node,Stack<Integer> pre){
        if(node.left==null&&node.right==null){
            pre.push(node.val);
            for(int i=pre.size()-1;i>=0;i--){
                res+=pre.get(i)*Math.pow(10,pre.size()-1-i);
            }
            pre.pop();
        }
        if(node.left!=null){
            pre.push(node.val);
            sumNumbersCore(node.left,pre);
            pre.pop();
        }
        if(node.right!=null){
            pre.push(node.val);
            sumNumbersCore(node.right,pre);
            pre.pop();
        }
    }
    public int sumNumbers(TreeNode root) {
        if(root==null)return 0;
        sumNumbersCore(root,new Stack<Integer>());
        return res;
    }
}
```
- 931.下降路径最小和  
dp(自底向上的动态规划)
```
class Solution {
    public int minFallingPathSum(int[][] A) {
        int len=A.length;
        if(len==0)return 0;
        int[] res=new int[len];
        for(int i=0;i<len;i++)res[i]=A[len-1][i];
        int[] temp=new int[len];
        for(int i=len-2;i>=0;i--){
            for(int j=0;j<len;j++){
                if(j==0){
                    temp[j]=A[i][j]+Math.min(res[j],res[j+1]);
                }else if(j==len-1){
                    temp[j]=A[i][j]+Math.min(res[j-1],res[j]);
                }else{
                    temp[j]=A[i][j]+Math.min(res[j],Math.min(res[j-1],res[j+1]));                    
                }
            }
            System.arraycopy(temp, 0, res, 0, len);
        }
        int min=res[0];
        for(int i:res)min=Math.min(min,i);
        return min;
    }
}
```
- 113.路径总和Ⅱ  
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
    private List<List<Integer>> res=new ArrayList<>();
    private void pathSumCore(TreeNode node,Stack<Integer> pre,int left){
        if(node.left==null&&node.right==null){
            if(left-node.val==0){
                pre.push(node.val);
                res.add(new ArrayList<Integer>(pre));
                pre.pop();
            }
            return;
        }
        if(node.left!=null){
            pre.push(node.val);
            pathSumCore(node.left,pre,left-node.val);
            pre.pop();
        }
        if(node.right!=null){
            pre.push(node.val);
            pathSumCore(node.right,pre,left-node.val);
            pre.pop();
        }
    }
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        if(root==null)return res;
        pathSumCore(root,new Stack<Integer>(),sum);
        return res;
    }
}
```
- 62.不同路径  
dp(自底向上的动态规划)
```
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp=new int[m][n];
        for(int i=m-1;i>=0;i--){
            for(int j=n-1;j>=0;j--){
                if(j!=n-1&&i==m-1){
                    dp[i][j]=1;
                }else if(j==n-1&&i!=m-1){
                    dp[i][j]=1;
                }else if(j==n-1&&i==m-1){
                    dp[i][j]=1;
                }else{
                    dp[i][j]=dp[i+1][j]+dp[i][j+1];
                }
            }
        }
        return dp[0][0];
    }
}
```
- 609.在系统中查找重复文件  **哈希表**
```
class Solution {
    public List<List<String>> findDuplicate(String[] paths) {
        HashMap<String,List<String> > map=new HashMap<>();
        for(String str:paths){
            String[] temp=str.split(" ");
            for(int i=1;i<temp.length;i++){
                String name=temp[i].substring(0,temp[i].indexOf("("));
                String content=temp[i].substring( temp[i].indexOf("(")+1,temp[i].indexOf(")") );
                if(map.containsKey(content)){
                    map.get(content).add(temp[0]+"/"+name);
                }else{
                    ArrayList<String> tempList=new ArrayList<String>();
                    tempList.add(temp[0]+"/"+name);
                    map.put(content,tempList);
                }
            }
        }
        List<List<String>> res=new ArrayList<>();
        for(Map.Entry<String, List<String> > entry : map.entrySet()){
            if(entry.getValue().size()>1){
                res.add(entry.getValue());
            }
        }
        return res;
    }
}
```
- 298.二叉树最长连续序列  
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
    private int max=0;
    private int longestConsecutiveCore(TreeNode node){
        if(node.left==null&&node.right==null){
            return 0;
        }
        int maxL=0,maxR=0;
        if(node.left!=null){
            if(node.val!=node.left.val-1){
                longestConsecutiveCore(node.left);
            }else{
                maxL=longestConsecutiveCore(node.left)+1;
            }
        }
        if(node.right!=null){
            if(node.val!=node.right.val-1){
                longestConsecutiveCore(node.right);
            }else{
                maxR=longestConsecutiveCore(node.right)+1;
            }
        }
        max=Math.max(Math.max(maxL,maxR),max);
        return Math.max(maxL,maxR);
    }
    public int longestConsecutive(TreeNode root) {
        if(root==null)return 0;
        longestConsecutiveCore(root);
        return max+1;
    }
}
```
