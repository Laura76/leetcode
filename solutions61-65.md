- 第六十一题 旋转列表
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head==null||head.next==null)return head;
        int len=1;
        ListNode oldTail=head;
        for(;oldTail.next!=null;len++)oldTail=oldTail.next;
        oldTail.next=head;
        int newTail=len-k%len-1;
        ListNode newHead=head;
        for(int i=0;i<=newTail;i++){
            if(i==newTail){
                oldTail=newHead;
            }
            newHead=newHead.next;
        }
        oldTail.next=null;
        return newHead;
    }
}
```
- 第六十二题 不同路径
```
class Solution {
    public int uniquePaths(int m, int n) {
        int[] col=new int[n];
        Arrays.fill(col,1);
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                col[j]+=col[j-1];
            }
        }
        return col[n-1];
    }
}
```
- 第六十三题 不同路径II
```
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int row=obstacleGrid.length;
        if(row==0)return 0;
        if(obstacleGrid[0][0]==1)return 0;
        int col=obstacleGrid[0].length;
        if(obstacleGrid[row-1][col-1]==1)return 0;
        int[] cols=new int[col];
        int[] rows=new int[row];
        cols[0]=1;rows[0]=1;
        for(int i=1;i<col;i++){
            if(obstacleGrid[0][i]==1){
                cols[i]=0;
            }else{
                cols[i]=cols[i-1];
            }
        }
        for(int i=1;i<row;i++){
            rows[i]=(obstacleGrid[i][0]==1)?0:rows[i-1];
        }
        for(int i=1;i<row;i++){
            for(int j=1;j<col;j++){
                if(obstacleGrid[i][j]==1){
                    cols[j]=0;
                }else{
                    if(j==1){
                        cols[j]+=rows[i];
                    }else{
                        cols[j]+=cols[j-1];
                    }
                }
            }
        }
        return cols[col-1];
    }
}
```
- 第六十四题 最小路径和
```
class Solution {
    public int minPathSum(int[][] grid) {
        int row=grid.length;
        if(row==0)return 0;
        int col=grid[0].length;
        int[] res=new int[col];
        res[col-1]=grid[row-1][col-1];
        int[] rows=new int[row];
        rows[row-1]=grid[row-1][col-1];
        //先确定一下边界的值
        for(int i=col-2;i>=0;i--){
            res[i]=grid[row-1][i]+res[i+1];
        }
        for(int i=row-2;i>=0;i--){
            rows[i]=grid[i][col-1]+rows[i+1];
        }
        for(int i=row-2;i>=0;i--){
            for(int j=col-2;j>=0;j--){
                if(j==col-2){
                    res[j]=grid[i][j]+Math.min(res[j],rows[i]);
                }else{
                    res[j]=grid[i][j]+Math.min(res[j],res[j+1]);
                }
            }
        }
        return res[0];
    }
}
```
- 第六十五题 有效数字 困难模式
