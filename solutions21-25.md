- 第二十一题 合并两个有序链表
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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode preHead=new ListNode(-1);
        ListNode pre=preHead;
        while(l1!=null&&l2!=null){
            if(l1.val<l2.val){
                pre.next=l1;
                l1=l1.next;
            }else{
                pre.next=l2;
                l2=l2.next;
            }
            pre=pre.next;
        }
        pre.next=(l1==null)?l2:l1;
        return preHead.next;
    }
}
```
- 第二十二题 括号生成 暂不处理
- 第二十三题 合并K个排序链表 困难题目
- 第二十四题 两两交换链表中的节点
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
    public ListNode swapPairs(ListNode head) {
        if(head==null||head.next==null){
            return head;
        }
        ListNode mute=new ListNode(-1);
        mute.next=head.next;
        head.next=swapPairs(head.next.next);
        mute.next.next=head;
        return mute.next;
    }
}
```
- 第二十五题 K个一组翻转链表
