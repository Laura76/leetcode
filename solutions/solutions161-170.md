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
- No.166 分数到小数
```
class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        if(numerator==0)return "0";
        StringBuilder builder=new StringBuilder();
        if(numerator<0^denominator<0){
            builder.append("-");
        }
        Long numeratorL=Math.abs(Long.valueOf(numerator));
        Long denominatorL=Math.abs(Long.valueOf(denominator));
        String quotient=String.valueOf((numeratorL/denominatorL));
        builder.append(quotient);
        Long remainder=(numeratorL%denominatorL);
        if(remainder==0)return builder.toString();
        builder.append(".");
        HashMap<Long,Integer> map=new HashMap<Long,Integer>();
        while(remainder!=0){
            if(map.containsKey(remainder)){
                builder.insert(map.get(remainder),"(");
                builder.append(")");
                break;
            }
            map.put(remainder,builder.length());
            remainder*=10;
            builder.append(remainder/denominatorL);
            remainder%=denominatorL;
        }
        return builder.toString();
    }
}
```
- No.167. 两数之和 II - 输入有序数组
```
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        for(int i=0;i<numbers.length;i++){
            map.put(numbers[i],i);
        }
        int[] res=new int[2];
        for(int i=0;i<numbers.length;i++){
            if(map.containsKey(target-numbers[i])&&(i!=map.get(target-numbers[i]))){
                res[0]=i>map.get(target-numbers[i])?map.get(target-numbers[i])+1:i+1;
                res[1]=i>map.get(target-numbers[i])?i+1:map.get(target-numbers[i])+1;
            }
        }
        return res;
    }
}
```
- No.168. Excel Sheet Column Title
```
class Solution {
    public String convertToTitle(int n) {
        HashMap<Integer,Character> map=new HashMap<Integer,Character>();
        for(int i=0;i<26;i++){
            map.put(i+1,(char)(65+i));
        }
        StringBuilder builder=new StringBuilder();
        while(n!=0){
            if(n%26!=0){
                builder.append(map.get(n%26));
                if(n/26<=26&&n/26>0){
                    builder.append(map.get(n/26));
                    break;
                }else{
                    n/=26;
                }
            }else {
                builder.append("Z");
                if((n/26-1)<=26&&(n/26-1)>0){
                    builder.append(map.get(n/26-1));
                    break;
                }else{
                    n=n/26-1;
                }
            }           
        }
        return builder.reverse().toString();
    }
}
```
- No.169. Majority Element
```
class Solution {
    public int majorityElement(int[] nums) {
        int times=nums.length/2;
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
            map.put(nums[i],map.getOrDefault(nums[i],0)+1);
            if(map.get(nums[i])>times)return nums[i];
        }
        return 0;
    }
}
```
- No.170 网站暂时崩掉了