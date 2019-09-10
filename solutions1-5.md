- 1.
```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        int complement=0;
        for(int i=0;i<nums.length;i++){
            complement=target-nums[i];
            if(map.containsKey(complement)){
              return new int[]{map.get(complement),i};
            }else{
              map.put(nums[i],i);
            }
        }
      return null;
    }
}
```
- 2.
```
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummyNode=new ListNode(0);
        ListNode curr=dummyNode;
        int carry=0;
        while(l1!=null||l2!=null){
          int x=(l1!=null)?l1.val:0;
          int y=(l2!=null)?l2.val:0;
          curr.next=new ListNode((x+y+carry)%10);
          carry=(x+y+carry)/10;
          curr=curr.next;
          if(l1!=null){
            l1=l1.next;
          }
          if(l2!=null){
            l2=l2.next;
          }
        }
        if(carry!=0){
          curr.next=new ListNode(carry);
        }
        return dummyNode.next;
    }
}
```
- 3.
```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int[] charSet=new int[128];
        for(int i=0;i<charSet.length;i++){
            charSet[i]=-1;
        }
        int i=0;
        int len=0;
        for(int j=0;j<s.length();j++){
            if(charSet[s.charAt(j)]==-1||charSet[s.charAt(j)]<i){
                charSet[s.charAt(j)]=j;
                len=Math.max(len,j-i+1);
            }else{
                i=charSet[s.charAt(j)]+1;
                charSet[s.charAt(j)]=j;
            }
        }
        return len;
    }
}
```
- 4.
```
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n=nums1.length;
        int m=nums2.length;
        int lo=0;int hi=2*n;
        int c1,c2=0;
        double lMax1=0.0,rMin1=0.0,lMax2=0.0,rMin2=0.0;
        if(n>m){
            //确保nums1为短的有序数组
            return findMedianSortedArrays(nums2,nums1);
        }else{
            //用二分法来找到nums1的切割点
            while(lo<=hi){
                c1=(lo+hi)/2;
                c2=m+n-c1;
                lMax1=(c1==0)?Integer.MIN_VALUE:nums1[(c1-1)/2];
                rMin1=(c1==2*n)?Integer.MAX_VALUE:nums1[c1/2];
                lMax2=(c2==0)?Integer.MIN_VALUE:nums2[(c2-1)/2];
                rMin2=(c2==2*m)?Integer.MAX_VALUE:nums2[c2/2];
                if(lMax1>rMin2){
                    hi--;
                }else if(lMax2>rMin1){
                    lo++;
                }else{
                    break;
                }
            }
        }
        double temp=Math.max(lMax1,lMax2)+Math.min(rMin1,rMin2);
        return temp/2;
    }
}
```
- 5.
```
class Solution {
    public String longestPalindrome(String s) {
        int len=s.length();
        if(len==0||len==1)return s;
        int max=1;
        int start=0;
        int[][] state=new int[len][len];
        for(int i=0;i<len;i++){
            state[i][i]=1;
        }
        for(int i=0;i<len-1;i++){
            if(s.charAt(i)==s.charAt(i+1)){
                state[i][i+1]=1;
                max=2;
                start=i;
            }
        }
        for(int l=3;l<=len;l++){
                for(int i=0;i+l-1<len;i++){
                    int end=i+l-1;
                    if(s.charAt(i)==s.charAt(end)&&state[i+1][end-1]==1){
                    state[i][end]=1;
                    max=l;
                    start=i;
                    }
                }
        }
        return s.substring(start,start+max);
        }
}
```
