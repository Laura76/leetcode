- No.141 环形链表 **双指针**  
快慢指针
```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head==null||head.next==null)return false;
        ListNode slow=head;
        ListNode fast=head.next;
        while(slow!=fast){
            if(fast.next==null||fast.next.next==null)return false;
            slow=slow.next;
            fast=fast.next.next;
        }
        return true;
    }
}
```
- No.142 环形链表Ⅱ  **Floyd算法**
```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    private ListNode isMeet(ListNode head){
        if(head==null)return null;
        ListNode tortoise=head;
        ListNode hare=head;
        while(hare!=null&&hare.next!=null){
            tortoise=tortoise.next;
            hare=hare.next.next;
            if(tortoise==hare){
                return tortoise;
            }
        }
        return null;
    }
    public ListNode detectCycle(ListNode head) {
        if(head==null||head.next==null)return null;
        ListNode meetFirst=isMeet(head);  
        if(meetFirst==null)return null;
        ListNode start1=head;
        while(start1!=meetFirst){
            start1=start1.next;
            meetFirst=meetFirst.next;
        }
        return start1;
    }
}
```
- N0.143 重排链表       
报内存限制的错误时：将一些废置的ListNode重新使用
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
    private ListNode reverseCore(ListNode node){
        if(node.next==null)return node;
        ListNode pre=reverseCore(node.next);
        node.next.next=node;
        node.next=null;
        return pre;
    }
    public void reorderList(ListNode head) {
        if(head==null||head.next==null)return;
        ListNode tor=head;
        ListNode hare=head;
        while(hare!=null&&hare.next!=null){
            tor=tor.next;
            hare=hare.next.next;
        }
        //递归逆转后半段链表
        ListNode h2=reverseCore(tor);
        //交替链接
        while(h2.next!=null&&head!=null){
            tor=head.next;
            hare=h2.next;
            head.next=h2;
            h2.next=tor;
            head=h2.next;
            h2=hare;
        }
    }
}
```
No.144 二叉树的前序遍历  **迭代实现** **栈**
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
    public List<Integer> preorderTraversal(TreeNode root) {
        Stack<TreeNode> stack=new Stack<TreeNode>();
        List<Integer> res=new LinkedList<Integer>();
        if(root==null)return res;
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node=stack.pop();
            res.add(node.val);
            if(node.right!=null){
                stack.push(node.right);
            }
            if(node.left!=null){
                stack.push(node.left);
            }
        }
        return res;
    }
}
```
No.145 二叉树的后序遍历 **困难**
