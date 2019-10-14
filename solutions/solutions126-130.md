- No.126 单词接龙II **困难**
- No.127 单词接龙 **BFS**
```
import javafx.util.Pair;
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        HashMap<String,ArrayList<String>> map=new HashMap<String,ArrayList<String>>();
        int level=0;
        for(String str:wordList){
            for(int i=0;i<str.length();i++){
                String temp=str.substring(0,i)+"*"+str.substring(i+1);
                ArrayList<String> strs=map.getOrDefault(temp,new ArrayList<String>());
                strs.add(str);
                map.put(temp,strs);
            }
        }
        Queue<Pair<String,Integer>> q=new LinkedList<>();
        q.add(new Pair(beginWord,1));
        HashMap<String,Boolean> visited=new HashMap<String,Boolean>();
        visited.put(beginWord,true);
        while(!q.isEmpty()){
            Pair<String,Integer> temp=q.remove();
            String key=temp.getKey();
            level=temp.getValue();
            for(int i=0;i<key.length();i++){
                String temp2=key.substring(0,i)+"*"+key.substring(i+1);
                for(String str:map.getOrDefault(temp2,new ArrayList<String>())){
                    if(str.equals(endWord)){
                        return level+1;
                    }
                    if(!visited.getOrDefault(str,false) ){
                        q.add(new Pair(str,level+1));
                        visited.put(str,true);
                    }
                }
            }
        }
        return 0;
    }
}
```
-No.128 最长连续序列 **困难**
-No.129 求根到叶子节点数字之和 **回溯**
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
    private List<String> pre=new LinkedList<String>();
    private void sumNumbersCore(TreeNode node,Stack<String> pre){
        if(node.left==null&&node.right==null){
            pre.push(String.valueOf(node.val));
            res+=Integer.valueOf(String.join("",pre));
            pre.pop();
            return;
        }
        if(node.left!=null){
            pre.push(String.valueOf(node.val));
            sumNumbersCore(node.left,pre);
            pre.pop();
        }
        if(node.right!=null){
            pre.push(String.valueOf(node.val));
            sumNumbersCore(node.right,pre);
            pre.pop();
        }

    }
    public int sumNumbers(TreeNode root) {
        if(root==null)return 0;
        sumNumbersCore(root,new Stack<String>());
        return res;
    }
}
```
- No. 被围绕的区域 **回溯** **dfs**
```
class Solution {
    private int row,col;
    //循环变为上下左右的回溯，在回溯中修改数组的值，但是不存储记录任何信息。
    private void dfs(int r,int c,char[][] board){
        if(r<0||r>=row||c<0||c>=col||board[r][c]=='X'||board[r][c]=='#'){
            return;
        }else{
            board[r][c]='#';
        }
        dfs(r-1,c,board);
        dfs(r,c+1,board);
        dfs(r+1,c,board);
        dfs(r,c-1,board);
    }
    public void solve(char[][] board) {
        int row=board.length;
        if(row==0)return;
        int col=board[0].length;
        this.row=row;this.col=col;
        for(int i=0;i<row;i++){
            for(int j=0;j<col;j++){
                boolean isEdge=(i==0||i==row-1||j==0||j==col-1);
                if(isEdge&&board[i][j]=='O'){
                    //可连通的O修改为#
                    dfs(i,j,board);
                }
            }
        }
        for(int i=0;i<row;i++){
            for(int j=0;j<col;j++){
                if(board[i][j]=='O')board[i][j]='X';
                else if(board[i][j]=='#')board[i][j]='O';
            }
        }
    }

}
```
