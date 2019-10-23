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
