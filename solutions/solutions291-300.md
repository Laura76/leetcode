- No.291 **氪金** **困难**
- No.292 Nim游戏 **dp**
```
class Solution {
    public boolean canWinNim(int n) {
        if(n==1||n==2||n==3)return true;
        int[] dp=new int[5];
        dp[0]=0;dp[1]=1;dp[2]=1;dp[3]=1;dp[4]=0;
        return dp[n%4]==1?true:false;
    }
}
```
- No.293 **氪金**
- No.294 **氪金**
- No.295 **困难**
- No.296 **氪金** **困难**
- No.297 **困难**
- No.298 **氪金**
- No.299 猜数字游戏
```
class Solution {
    public String getHint(String secret, String guess) {
        int len=secret.length();
        HashMap<Character,Integer> map=new HashMap<Character,Integer>();
        for(int i=0;i<len;i++){
            char temp=secret.charAt(i);
            map.put(temp,map.getOrDefault(temp,0)+1);
        }
        int countA=0,countB=0;
        //先处理位置数字都相同的情况
        for(int i=0;i<guess.length();i++){
            char temp=guess.charAt(i);
            if(temp==secret.charAt(i)){
                countA++;
                map.put(temp,map.get(temp)-1);
            }
        }
        for(int i=0;i<guess.length();i++){
            char temp=guess.charAt(i);
            if(temp!=secret.charAt(i)){
                if(map.containsKey(temp)&&map.get(temp)!=0){
                    countB++;
                    map.put(temp,map.get(temp)-1);
                }
            }
        }
        return countA+"A"+countB+"B";
    }
}
```
- No.300 最长上升子序列  **dp**
```
class Solution {
    public int lengthOfLIS(int[] nums) {
        int len=nums.length;
        if(len==0)return 0;
        //以nums[i]结尾的序列的长度
        int[] dp=new int[len];
        for(int i=0;i<len;i++)dp[i]=1;
        for(int i=1;i<len;i++){
            for(int j=0;j<i;j++){
                if(nums[i]>nums[j]){
                    dp[i]=Math.max(dp[i],dp[j]+1);
                }
            }     
        }
        int res=0;
        for(int i:dp)res=Math.max(res,i);
        return res;
    }
}
```
