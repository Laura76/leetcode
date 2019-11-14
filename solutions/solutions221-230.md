-  No.221 最大正方形  **dp**  
最小问题是以当前的元素为右下角元素的最大的正方形
```
class Solution {
    public int maximalSquare(char[][] matrix) {
        int row=matrix.length;
        if(row==0)return 0;
        int col=matrix[0].length;
        int res=0;
        for(int i=0;i<row;i++){
            for(int j=0;j<col;j++){
                if(matrix[i][j]!='1')continue;
                if(i==0||j==0){
                    res=Math.max(res,1);
                }else{
                    matrix[i][j]=(char)(Math.min(matrix[i-1][j]-'0',Math.min(matrix[i-1][j-1]-'0',matrix[i][j-1]-'0'))+'1');
                    res=Math.max(res,matrix[i][j]-'0');
                }             
            }
        }
        return res*res;
    }
}
```
- No.222 完全二叉树的节点个数  
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
    public int countNodes(TreeNode root) {
        Queue<TreeNode> q=new LinkedList<TreeNode>();
        if(root==null)return 0;
        int res=1;
        q.add(root);
        while(!q.isEmpty()){
            TreeNode temp=q.remove();
            if(temp.left!=null){
                q.add(temp.left);res++;
            }
            if(temp.right!=null){
                q.add(temp.right);res++;
            }
        }
        return res;
    }
}
```
- No.223 矩形面积  
```
class Solution {
    public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        int sum=(C-A)*(D-B)+(H-F)*(G-E);
        if(E>=C||G<=A||F>=D||H<=B)return sum;
        int overlap=(Math.min(C,G)-Math.max(A,E))*(Math.min(D,H)-Math.max(B,F));
        return sum-overlap;
    }
}
```
- No.224 基本计算器  **困难**
- No.225 用队列实现栈  **双队列**
```
class MyStack {
    private Queue<Integer> q1;
    private Queue<Integer> q2;
    private int peek;
    /** Initialize your data structure here. */
    public MyStack() {
        q1=new LinkedList<Integer>();
        q2=new LinkedList<Integer>();
    }

    /** Push element x onto stack. */
    public void push(int x) {
        q1.add(x);
        peek=x;
    }

    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        int temp=q1.remove();       
        while(!q1.isEmpty()){
            q2.add(temp);
            temp=q1.remove();
        }
        if(!q2.isEmpty()){
            int temp2=q2.remove();           
            while(!q2.isEmpty()){
                q1.add(temp2);
                temp2=q2.remove();
            }
            q1.add(temp2);
            peek=temp2;
        }       
        return temp;
    }

    /** Get the top element. */
    public int top() {
        return peek;
    }

    /** Returns whether the stack is empty. */
    public boolean empty() {;
        return q1.isEmpty();
    }
}
/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```
- No.226 翻转二叉树  **递归**
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
    public TreeNode invertTree(TreeNode root) {    
        if(root==null)return root;  
        TreeNode temp=root.left;
        if(root.left!=null){
            temp=invertTree(root.left);
        }
        if(root.right!=null)invertTree(root.right);
        root.left=root.right;
        root.right=temp;
        return root;

    }
}
```
