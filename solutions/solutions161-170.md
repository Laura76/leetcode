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
- No.163 缺失的区间  
超出最大值的情况要考虑
```
class Solution {
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        List<String> res=new LinkedList<String>();
        int len=nums.length;
        for(int i=0;i<len;i++){
            if(nums[i]==lower){
                if(nums[i]<Integer.MAX_VALUE)lower++;
                else break;
            }
            else if(nums[i]==lower+1){
                res.add(String.valueOf(lower));
                if(nums[i]<Integer.MAX_VALUE-1)lower+=2;
                else break;              
            }else if(nums[i]>lower+1){
                res.add(String.valueOf(lower)+"->"+String.valueOf(nums[i]-1));                if(nums[i]<=Integer.MAX_VALUE-1)lower=nums[i]+1;
                else break;               
            }
        }
        if(len==0||nums[len-1]<upper){
            if(lower<upper)
                res.add(String.valueOf(lower)+"->"+String.valueOf(upper));
            else if(lower==upper)                res.add(String.valueOf(lower));
        }
        return res;
    }
}
```
- No.164 最大间距 **困难**
- No.165 比较版本号
```
class Solution {
    public int compareVersion(String version1, String version2) {
        String[] v1=version1.split("\\.");
        String[] v2=version2.split("\\.");
        for(int i=0;i<v1.length&&i<v2.length;i++){
            if(Integer.valueOf(v1[i])>Integer.valueOf(v2[i]))return 1;
            else if(Integer.valueOf(v1[i])<Integer.valueOf(v2[i]))return -1;
        }
        if(v1.length>v2.length){
            for(int i=v2.length;i<v1.length;i++){
                if(Integer.valueOf(v1[i])>0)return 1;
            }
            return 0;
        }
        else if(v1.length==v2.length) return 0;
        else {
            for(int i=v1.length;i<v2.length;i++){
                if(Integer.valueOf(v2[i])>0)return -1;
            }
            return 0;
        }
    }
}
```