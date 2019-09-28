- 第九十一题 解码方法
使用动态规划的方法，但是有很多的小细节导致我提交了很多次。但是毕竟是第一次使用动态规划成功嘿嘿～今天的外教依旧很尬呃呃呃呃
```
class Solution {
    public int numDecodings(String s) {
        if(s.startsWith("0"))return 0;
        char[] nums=s.toCharArray();
        int len=nums.length;
        if(len==1&&Integer.valueOf(s)==0)return 0;
        int[] dp=new int[len+1];
        dp[0]=1;
        dp[1]=1;
        for(int i=2;i<=len;i++){
            dp[i]=nums[i-1]=='0'?0:dp[i-1];
            int temp=Integer.valueOf(s.substring(i-2,i));
            if(temp<=26&&temp>=10){
                dp[i]+=dp[i-2];
            }
        }
        return dp[len];
    }
}
```