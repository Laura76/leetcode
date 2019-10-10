- 第二十六题 删除排序数组中重复项
```
class Solution {
    public int removeDuplicates(int[] nums) {
        int len=nums.length;
        int i=0;
        for(int j=1;j<len;j++){
            if(nums[j]!=nums[i]){
                i++;
                nums[i]=nums[j];
            }
        }
        return i+1;
    }
}
```
- 第二十七题 移除元素
```
class Solution {
    public int removeElement(int[] nums, int val) {
        int res=0;
        int len=nums.length;
        for(int i=0;i<len;i++){
            if(nums[i]!=val){
                nums[res]=nums[i];
                res++;
            }
        }
        return res;
    }
}
```
- 第二十八题 实现str Str()
```
class Solution {
    public int strStr(String haystack, String needle) {
        int len=needle.length();
        for(int i=0;i<=haystack.length()-len;i++){
            if(haystack.substring(i,i+len).equals(needle)){
                return i;
            }
        }
        return -1;
    }
}
```
- 第二十九题 两数相除
```
class Solution {
    public int divide(int dividend, int divisor) {
        if(dividend==0)return 0;
        if(dividend==Integer.MIN_VALUE&&divisor==-1)return Integer.MAX_VALUE;
        long dividendLong=Math.abs((long)dividend);
        long divisorLong=Math.abs((long)divisor);
        int res=0;
        for(int i=31;i>=0;i--){
            if((dividendLong>>i)>=divisorLong){
                res+=(1<<i);
                dividendLong-=divisorLong<<i;
            }
        }
        res=(dividend^divisor)<0?-res:res;
        return res;
    }
}
```
- 第三十题 困难 不要嘛