- No.161 相隔为 1 的编辑距离
```
class Solution {
    public boolean isOneEditDistance(String s, String t) {
        if(s.equals(t))return false;
        int sLen=s.length();
        int tLen=t.length();
        if(sLen-tLen==-1){
            for(int i=0;i<=sLen;i++){
                if(s.substring(0,i).equals(t.substring(0,i))&&s.substring(i).equals(t.substring(i+1))){
                    return true;
                }
            }
        }else if(sLen-tLen==1){
            for(int i=0;i<sLen;i++){
                if(s.substring(0,i).equals(t.substring(0,i))&&s.substring(i+1).equals(t.substring(i))){
                    return true;
                }
            }
        }else if(sLen==tLen){
             for(int i=0;i<sLen;i++){
                if(s.substring(0,i).equals(t.substring(0,i))&&s.substring(i+1).equals(t.substring(i+1))){
                    return true;
                }
            }
        }
        return false;
    }
}
```
- No.162 寻找峰值
```
class Solution {
    public int findPeakElement(int[] nums) {
        int len=nums.length;
        if(len==1)return 0;
        if(nums[0]>nums[1])return 0;
        for(int i=1;i<len-1;i++){
            if(nums[i]>nums[i-1]&&nums[i]>nums[i+1])return i;
        }
        if(nums[len-1]>nums[len-2])return len-1;
        return 0;
    }
}
```
