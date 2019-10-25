- No.151 翻转字符串里的单词  **栈**
```
class Solution {
    public String reverseWords(String s) {
        Stack<String> stack=new Stack<String>();
        StringBuilder builder=new StringBuilder();
        for(int i=0;i<s.length();i++){
            while(i<s.length()&&s.charAt(i)==' ')i++;
            int start=i;i++;
            while(i<s.length()&&s.charAt(i)!=' ')i++;
            if(start<s.length())stack.push(s.substring(start,i));
        }
        while(!stack.isEmpty()){
            builder.append(stack.pop());
            builder.append(" ");
        }
        if(builder.length()>0)builder.deleteCharAt(builder.length()-1);
        return builder.toString();
    }
}
```
- No.152 乘积最大子序列  **dp**
要大胆地dp
```
class Solution {
    public int maxProduct(int[] nums) {
        int len=nums.length;
        if(len==0)return 0;
        int res=nums[0];
        int pre_max=nums[0];int pre_min=nums[0];
        for(int i=1;i<len;i++){
            int temp=pre_max;
            pre_max=Math.max(Math.max(pre_max*nums[i],nums[i]),pre_min*nums[i]);
            pre_min=Math.min(Math.min(temp*nums[i],nums[i]),pre_min*nums[i]);
            res=Math.max(res,pre_max);
        }
        return res;
    }
}
```
- No.153 寻找旋转排序数组中的最小值 **二分法**
```
class Solution {
    public int findMin(int[] nums) {
        int len=nums.length;
        if(len==1)return nums[0];
        int left=0;int right=len-1;
        if(nums[right]>nums[left])return nums[0];
        while(left<right){
            int mid=left+((right-left)>>1);
            if(nums[mid]>nums[mid+1])return nums[mid+1];
            if(nums[mid-1]>nums[mid])return nums[mid];
            if(nums[mid]>nums[0])left=mid+1;
            if(nums[mid]<nums[0])right=mid-1;
        }
        return -1;
    }
}
```
- No.154 寻找旋转排序数组中的最小值II **困难**  
- No.155 最小栈  **辅助栈**  
我真的搞不懂了，直接使用两个stack的peek()来比较怎么就一直是false呢。
```
class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> min;
    /** initialize your data structure here. */
    public MinStack() {
        this.stack=new Stack<Integer>();
        this.min=new Stack<Integer>();
    }
    public void push(int x) {
        if(stack.isEmpty()||x<=min.peek())min.push(x);
        stack.push(x);
    }

    public void pop() {
        int temp1=stack.peek();
        int temp2=min.peek();
        if(temp1==temp2){
            min.pop();
        }
        stack.pop();
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return min.peek();
    }
}
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
 ```
- No.156 上下翻转二叉树  **递归**
```
class Solution {
    public TreeNode upsideDownBinaryTree(TreeNode root) {
        //找到最左节点，再进行指针操作，再递归
        if(root==null||(root.left==null&&root.right==null))return root;
        TreeNode pre=root;TreeNode cur=root;
        while(cur.left!=null||cur.right!=null){
            pre=cur;
            cur=cur.left;
        }
        cur.left=pre.right;
        pre.right=pre.left=null;
        cur.right=upsideDownBinaryTree(root);
        return cur;
    }
}
```
- No.157  用 Read4 读取 N 个字符  
很烦
```
/**
 * The read4 API is defined in the parent class Reader4.
 *     int read4(char[] buf);
 */
public class Solution extends Reader4 {
    /**
     * @param buf Destination buffer
     * @param n   Number of characters to read
     * @return    The number of actual characters read
     */
    public int read(char[] buf, int n) {
        int numCount=0;int start=0;
        char[] help=new char[4];
        while(numCount<n){
            int temp=read4(help);
            if(temp%4!=0){
                for(int i=0;i<Math.min(n-numCount,temp);i++)buf[start++]=help[i];
                numCount+=Math.min(n-numCount,temp);
                break;
            }
            if(temp!=0&&(n-numCount)<4){
                for(int i=0;i<n-numCount;i++)buf[start++]=help[i];
                numCount+=(n-numCount);
            }else{
                for(int i=0;i<4;i++)buf[start++]=help[i];
                numCount+=temp;
            }
            if(temp%4!=0||temp==0)break;
        }
        return numCount;
    }
}
```
- No.158 用 Read4 读取 N 个字符 II  **困难**
- No.159 至多包含两个不同字符的最长子串  **困难**
- No.160. 相交链表
```
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode p1=headA,p2=headB;
        while(p1!=null||p2!=null){
            if(p1==p2)return p1;
            if(p1==null)p1=headB;
            else p1=p1.next;
            if(p2==null)p2=headA;
            else p2=p2.next;
        }
        return null;
    }
}
```
