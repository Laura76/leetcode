- No.261 **氪金**
- No.262 行程和用户 **困难**
- No.263 丑数
```
class Solution {
    public boolean isUgly(int num) {
        if(num==0)return false;
        while(true){
            if(num==1)return true;
            if(num%5!=0&&num%3!=0&&num%2!=0)return false;             
            if(num%5==0)num=num/5;
            else if(num%3==0)num=num/3;
            else if(num%2==0)num=num/2;            
        }
    }
}
```
- No.264 丑数II **dp+三指针**  
注意：例如像6这样的既可以是2*3也可以是3*2的构成，那么要2和3的指针都要向前推进一步。
```
class Solution {
    public int nthUglyNumber(int n) {
        int click1=0,click2=0,click3=0;
        int[] dp=new int[n];
        dp[0]=1;
        for(int i=1;i<n;i++){
            int min=Math.min(dp[click1]*2,Math.min(dp[click2]*3,dp[click3]*5));
            if(min==dp[click1]*2)click1++;
            if(min==dp[click2]*3)click2++;
            if(min==dp[click3]*5)click3++;
            dp[i]=min;
        }
        return dp[n-1];
    }
}
```
- No.265 粉刷房子 II  **氪金+困难**
- No.266-267  **氪金**
- No.268 缺失数字
```
class Solution {
    public int missingNumber(int[] nums) {
        Arrays.sort(nums);
        int start=0;
        for(int i:nums){
            if(i!=(start++))return start-1;
        }
        return start;
    }
}
```
- No.269-270  **氪金**
