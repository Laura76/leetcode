- 第八十一题 搜索旋转排序数组Ⅱ
不想使用简单的顺序查找完成，又不想使用二分法，我讨厌二分法裹脚布一样繁琐的细节和边界处理。
- 第八十二题 删除排序链表中的重复元素Ⅱ
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
    public ListNode deleteDuplicates(ListNode head) {
        if(head==null||head.next==null)return head;
        ListNode pr=head;
        ListNode pc=head.next;
        ListNode pBefore=head;
        while(pc!=null){
            if(pc.val!=pr.val){
                pBefore=pr;
                pr=pr.next;
                pc=pc.next;
            }else{
                while(pc!=null&&pc.val==pr.val){
                    pc=pc.next;
                }
                if(pc==null){
                    if(pBefore==head&&pr==head){
                        return null;
                    }else{
                        pBefore.next=null;
                    }
                }else{
                    if(pBefore==head&&pr==head){
                        pBefore=pc;
                        head=pBefore;
                    }else{
                        pBefore.next=pc;
                    }
                    pr=pc;
                    pc=pc.next;
                }
            }
        }
        pr.next=null;
        return head;
    }
}
```
- 第八十三题 删除排序链表中的重复元素
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
    public ListNode deleteDuplicates(ListNode head) {
        if(head==null)return head;
        ListNode pr=head;
        ListNode pc=head;
        while(pc!=null){
            if(pc.val==pr.val){
                pc=pc.next;
            }else{
                pr.next=pc;
                pr=pc;
                pc=pc.next;
            }
        }
        pr.next=null;
        return head;
    }
}
```
- 第八十四题 柱状图中最大的矩形 困难模式不要啦
- 第八十五题 最大矩形 困难模式 怎么看到困难有点开心不用做
