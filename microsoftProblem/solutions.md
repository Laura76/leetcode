- 1.两数之和  
哈希表
```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] res=new int[2];
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
            map.put(nums[i],i);
        }
        for(int i=0;i<nums.length;i++){
            if(map.containsKey(target-nums[i])&&map.get(target-nums[i])!=i){
                res[0]=i;res[1]=map.get(target-nums[i]);
                return res;
            }
        }
        return res;
    }
}
```
- 2.两数相加  
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int cur=(l1.val+l2.val)%10;
        int carry=(l1.val+l2.val)>=10?1:0;
        ListNode res=new ListNode(cur);
        ListNode temp=res;
        while(l1.next!=null&&l2.next!=null){
            l1=l1.next;l2=l2.next;
            cur=(l1.val+l2.val+carry)%10;
            carry=(l1.val+l2.val+carry)>=10?1:0;
            res.next=new ListNode(cur);
            res=res.next;
        }
        while(l1.next!=null){
            l1=l1.next;
            cur=(l1.val+carry)%10;
            carry=(l1.val+carry)>=10?1:0;
            res.next=new ListNode(cur);
            res=res.next;
        }
        while(l2.next!=null){
            l2=l2.next;
            cur=(l2.val+carry)%10;
            carry=(l2.val+carry)>=10?1:0;
            res.next=new ListNode(cur);
            res=res.next;
        }
        if(carry==1){
            res.next=new ListNode(1);
        }
        return temp;
    }
}
```
- 3.无重复字符的最长字串  
为什么会卡很久
```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashMap<Character,Integer> map=new HashMap<Character,Integer>();
        int left=0,max=0;
        for(int i=0;i<s.length();i++){
            char temp=s.charAt(i);
            if(!map.containsKey(temp)||(map.containsKey(temp)&&map.get(temp)<left)){
                max=Math.max(i-left+1,max);
            }else{
                if(map.get(temp)>=left)left=map.get(temp)+1;
            }
            map.put(temp,i);
        }
        return max;
    }
}
```
- 4.寻找两个有序数组的中位数  **困难**
- 5.最长回文子串  **dp**
```
class Solution {
    public String longestPalindrome(String s) {
        int len=s.length();
        String res="";
        if(len==0)return res;
        //数组表示从下标A到下标B的字符串是否是回文，是则为1
        int[][] dp=new int[len][len];
        int left=0,right=0;
        //初始化dp数组
        for(int i=0;i<len;i++){
            dp[i][i]=1;
            if(i==len-1)break;
            else{
                if(s.charAt(i)==s.charAt(i+1)){
                    dp[i][i+1]=1;
                    left=i;right=i+1;
                }
            }
        }
        //遍历
        for(int i=3;i<=len;i++){
            for(int j=0;j+i-1<=len-1;j++){
                if(s.charAt(j)==s.charAt(j+i-1)&&dp[j+1][j+i-2]==1){
                    dp[j][j+i-1]=1;
                    left=j;right=j+i-1;
                }
            }
        }
        res=s.substring(left,right+1);
        return res;
    }
}
```
