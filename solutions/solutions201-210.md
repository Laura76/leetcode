- No.201 数字范围按位与  **数学**
```
class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        if(m==n)return m;
        int count=0;
        while(m!=n){
            m>>=1;
            n>>=1;
            count++;
        }
        return m<<=count;
    }
}
```
- No.202 欢乐数  **数学**
```
class Solution {
    private int isHappyCore(int n){
        int res=0;
        while(n!=0){
            res+=Math.pow(n%10,2);
            n/=10;
        }
        return res;
    }
    public boolean isHappy(int n) {
        int slow=n,fast=n;
        do{
            slow=isHappyCore(slow);
            fast=isHappyCore(fast);
            fast=isHappyCore(fast);
        }while(slow!=fast);
        return slow==1;
    }
}
```
- No.203 移除链表元素  **快慢指针**
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
    public ListNode removeElements(ListNode head, int val) {
        ListNode befo=head;
        if(head==null)return head;
        ListNode node=head.next;
        while(node!=null){
            if(node.val==val){
                befo.next=node.next;
            }else{
                befo=befo.next;
            }
            node=node.next;

        }
        if(head.val==val)return head.next;
        return head;
    }
}
```
- No.204 计数质数  **素数**
```
class Solution {
    public int countPrimes(int n) {
        int[] isPrime=new int[n];
        Arrays.fill(isPrime,-1);
        int res=0;
        for(int i=2;i<n;i++){
            if(isPrime[i]==-1&&isPrimeCore(i)==true){
                res++;isPrime[i]=0;
                for(int j=2;j*i<n;j++){
                    isPrime[i*j]=1;
                }
            }
        }
        return res;
    }
    private boolean isPrimeCore(int n){
        if(n==2)return true;
        for(int i=2;i*i<n;i++){
            if(n%i==0)return false;
        }
        return true;
    }
}
```
- No.205 同构字符串  **哈希表**
```
class Solution {
    public boolean isIsomorphic(String s, String t) {
        int sLen=s.length(),tLen=t.length();
        if(sLen!=tLen)return false;
        boolean res=true;
        HashMap<Character,Integer> smap=new HashMap<Character,Integer>();
        HashMap<Character,Integer> tmap=new HashMap<Character,Integer>();
        for(int i=0;i<sLen;i++){
            smap.put(s.charAt(i),smap.getOrDefault(s.charAt(i),i));
            tmap.put(t.charAt(i),tmap.getOrDefault(t.charAt(i),i));
            if(smap.get(s.charAt(i))!=tmap.get(t.charAt(i)))return false;
        }
        return res;
    }
}
```
- No.206 反转链表  **迭代**
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
    public ListNode reverseList(ListNode head) {
        ListNode pre=null;
        ListNode cur=head;
        while(cur!=null){
            ListNode temp=cur.next;
            cur.next=pre;
            pre=cur;
            cur=temp;
        }
        return pre;
    }
}
```
