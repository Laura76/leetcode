- No.231 2的幂  **循环除以二**
```
class Solution {
    public boolean isPowerOfTwo(int n) {
        if(n==0)return false;
        if(n==1)return true;
        while(n%2==0)n=n/2;
        if(n!=1)return false;
        else return true;
    }
}
```
- No.232 用栈实现队列  **辅助栈**
```
class MyQueue {
    private Stack<Integer> stack;
    private Stack<Integer> helpStack;
    /** Initialize your data structure here. */
    public MyQueue() {
        stack=new Stack<Integer>();
        helpStack=new Stack<Integer>();
    }

    /** Push element x to the back of queue. */
    public void push(int x) {
        while(!stack.isEmpty())helpStack.push(stack.pop());
        stack.push(x);
        while(!helpStack.isEmpty())stack.push(helpStack.pop());
    }

    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        return stack.pop();
    }

    /** Get the front element. */
    public int peek() {
        return stack.peek();
    }

    /** Returns whether the queue is empty. */
    public boolean empty() {
        return stack==null||stack.isEmpty();
    }
}
/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```
- No.233 数字 1 的个数  
- No.234 回文链表
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
    public boolean isPalindrome(ListNode head) {
        Stack<Integer> s=new Stack<Integer>();
        ListNode temp=head;
        while(temp!=null){
            s.push(temp.val);
            temp=temp.next;
        }
        while(head!=null){
            if(s.pop()!=head.val)return false;
            head=head.next;
        }
        return true;
    }
}
```
- No.235 二叉搜索树的最近公共祖先  **dfs**  
我好强啊
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
    private TreeNode res;
    //返回值：该子树中是否具有节点p或者q
    public boolean dfs(TreeNode node,TreeNode p,TreeNode q){
        boolean hasPQ=false;
        if(node==p||node==q)hasPQ=true;
        boolean leftHas=false,rightHas=false;
        if(node.left!=null){
            leftHas=dfs(node.left,p,q);
        }
        if(leftHas==true)hasPQ=true;
        if(node.right!=null){
            rightHas=dfs(node.right,p,q);
        }
        if(rightHas==true)hasPQ=true;
        if(node==p||node==q){
            if(leftHas==true||rightHas==true){
                res=node;
            }
        }else{
            if(leftHas==true&&rightHas==true){
                res=node;
            }
        }
        return hasPQ;
    }
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        dfs(root,p,q);
        return res;
    }
}
```
- No.236 二叉树的最近公共祖先  **dfs**  
同上一题一样的解答  
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
    private TreeNode res;
    //返回值：该子树中是否具有节点p或者q
    public boolean dfs(TreeNode node,TreeNode p,TreeNode q){
        boolean hasPQ=false;
        if(node==p||node==q)hasPQ=true;
        boolean leftHas=false,rightHas=false;
        if(node.left!=null){
            leftHas=dfs(node.left,p,q);
        }
        if(leftHas==true)hasPQ=true;
        if(node.right!=null){
            rightHas=dfs(node.right,p,q);
        }
        if(rightHas==true)hasPQ=true;
        if(node==p||node==q){
            if(leftHas==true||rightHas==true){
                res=node;
            }
        }else{
            if(leftHas==true&&rightHas==true){
                res=node;
            }
        }
        return hasPQ;
    }
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        dfs(root,p,q);
        return res;
    }
}
```
- No.237 删除链表中的节点    
傻逼题目，传入的参数是链表中的节点，删除该节点就是：把该节点的值改成下一个节点的值，该节点的指针改成下一个节点的指针。
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
    public void deleteNode(ListNode node) {
        node.val=node.next.val;
        node.next=node.next.next;
    }
}
```
- No.238 除自身以外数组的乘积  **左积乘右积**
```
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int len=nums.length;
        int[] res=new int[len];
        int k=nums[0];
        for(int i=1;i<len;i++){
            res[i]=k;
            k*=nums[i];
        }
        k=nums[len-1];
        for(int i=len-2;i>0;i--){
            res[i]*=k;
            k*=nums[i];
        }
        res[0]=k;
        return res;
    }
}
```
- No.239 滑动窗口最大值  **困难**
- No.240 搜索二维矩阵 II  
```
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m=matrix.length;
        if(m==0)return false;
        int n=matrix[0].length;
        if(n==0)return false;
        int row=0,col=n-1;
        while(true){
            if(matrix[row][col]==target)return true;
            else if(matrix[row][col]<target)row++;
            else if(matrix[row][col]>target)col--;
            if(row>=m||col<0)return false;
        }
    }
}
```
