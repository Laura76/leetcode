- No.191 位1的个数  **位运算**
```
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int res=0;
        for(int i=0;i<=31;i++){
            int temp=(n>>i);
            temp=temp&1;
            if(temp==1)res++;
        }
        return res;
    }
}
```
- No.192 统计词频  **Bash**
- No.193 有效电话号码  **Bash**
- No.194 转置文件  **Bash**
- No.195 第十行  **Bash**
- No.196 删除重复的电子邮箱  **使用子查询避开这样的错误：不允许同视查询和删除同一张表**
```
# Write your MySQL query statement below
delete from  Person
where Person.Id in(
    select Id from(
select p1.Id Id
from Person p1,Person p2
where p1.Email=p2.Email and p1.Id>p2.Id
) a                
    )
```
- No.197 上升的温度
```
/* Write your PL/SQL query statement below */
select w2.Id
from Weather w1,Weather w2
where w1.RecordDate+1=w2.RecordDate and w1.Temperature<w2.Temperature
```
- No.198 打家劫舍 **dp**
为什么一道动态规划的题目等级是简单，我又为什么一道简单的题想不到动态规划，到底谁把谁看太轻，谁把谁看太重。
```
class Solution {
    public int rob(int[] nums) {
        int len=nums.length;
        int[] dp=new int[len+1];
        if(len==0)return 0;
        dp[1]=nums[0];
        if(len==1)return dp[1];
        dp[2]=Math.max(nums[0],nums[1]);
        for(int i=3;i<=len;i++){
            dp[i]=Math.max(dp[i-1],dp[i-2]+nums[i-1]);
        }
        return dp[len];
    }
}
```
- No.199 二叉树的左视图  **一个辅助的queue来记录二叉树的层数**
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
    public List<Integer> rightSideView(TreeNode root) {
        Queue<TreeNode> q=new LinkedList<TreeNode>();
        Queue<Integer> depth=new LinkedList<Integer>();
        List<Integer> res=new ArrayList<Integer>();
        if(root==null)return res;
        q.add(root);depth.add(1);
        while(!q.isEmpty()){
            if(q.peek().left!=null){
                q.add(q.peek().left);
                depth.add(depth.peek()+1);
            }
            if(q.peek().right!=null){
                q.add(q.peek().right);
                depth.add(depth.peek()+1);
            }
            TreeNode temp=q.remove();
            if(depth.remove()!=depth.peek()){
                res.add(temp.val);
            }
        }
        return res;
    }
}
```
- No.200 岛屿数量  **dfs**  
回溯递归的深度优先遍历
```
class Solution {
    private int[] direcR={-1,0,1,0};
    private int[] direcC={0,1,0,-1};
    private int row,col;
    private void numIslandsCore(char[][] grid,int row,int col){
        for(int i=0;i<4;i++){
            int tempR=row+direcR[i],tempC=col+direcC[i];
            if(tempR>=0&&tempR<this.row&&tempC>=0&&tempC<this.col){
                if(grid[row+direcR[i]][col+direcC[i]]=='1'){
                    grid[row+direcR[i]][col+direcC[i]]='2';
                    numIslandsCore(grid,row+direcR[i],col+direcC[i]);
                }
            }
        }
        grid[row][col]='2';

    }
    public int numIslands(char[][] grid) {
        int res=0;
        if(grid.length==0)return 0;
        this.row=grid.length;this.col=grid[0].length;
        for(int i=0;i<grid.length;i++){
            for(int j=0;j<grid[0].length;j++){
                //访问过的被置为2
                if(grid[i][j]=='1'){
                    numIslandsCore(grid,i,j);
                    res++;
                }
            }
        }
        return res;
    }
}
```
