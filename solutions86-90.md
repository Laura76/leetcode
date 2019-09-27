- 第八十六题 分隔链表
有一个巨坑，要把最后一个元素必须记得指向null，导致报：内存限制错误 。
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
    public ListNode partition(ListNode head, int x) {
        if(head==null||head.next==null)return head;
        ListNode prBefore=new ListNode(-1);
        ListNode prBeforeHead=prBefore;
        ListNode prAfter=new ListNode(-1);
        ListNode prAfterHead=prAfter;
        ListNode pc=head;
        while(pc!=null){
            if(pc.val<x){
                if(prBeforeHead.val==-1){
                    prBeforeHead=pc;
                    prBefore=pc;
                }else{
                    prBefore.next=pc;
                    prBefore=pc;
                }
            }else{
                if(prAfterHead.val==-1){
                    prAfterHead=pc;
                    prAfter=pc;
                }else{
                    prAfter.next=pc;
                    prAfter=pc;
                }
            }
            pc=pc.next;
        }
        prBefore.next=prAfterHead.val==-1?null:prAfterHead;
        prAfter.next=null;
        return prBeforeHead.val==-1?prAfterHead:prBeforeHead;
    }
}
```
- 第八十七题 扰乱字符串 困难模式
- 第八十八题 合并两个有序数组
```
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int len=nums1.length;
        int pr=len-1;
        int start1=m-1;
        int start2=n-1;
        while(start1>=0&&start2>=0){
            if(nums1[start1]>nums2[start2]){
                nums1[pr]=nums1[start1];
                pr--;
                start1--;
            }else{
                nums1[pr]=nums2[start2];
                pr--;
                start2--;
            }
        }
        if(start1<0&&start2>=0){
            while(start2>=0){
                nums1[pr]=nums2[start2];
                start2--;
                pr--;
            }
        }else if(start2<0&&start1>=0){
            while(start1>=0){
                nums1[pr]=nums1[start1];
                start1--;
                pr--;
            }
        }
        pr++;
        for(int i=0;i<m+n;i++){
            nums1[i]=nums1[pr+i];
        }
    }
}
``
- 第八十九题 格雷编码
```
```
