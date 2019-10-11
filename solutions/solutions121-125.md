- No.121 买卖股票的最佳时机  **动态规划**  
真的很漂亮的动态规划
```
class Solution {
    public int maxProfit(int[] prices) {
        int len=prices.length;
        if(len==0)return 0;
        int[][] dp=new int[len][2];
        dp[0][0]=0;
        dp[0][1]=-prices[0];
        for(int i=1;i<len;i++){
            dp[i][0]=Math.max(dp[i-1][0],dp[i-1][1]+prices[i]);
            dp[i][1]=Math.max(-prices[i],dp[i-1][1]);
        }
        return dp[len-1][0];
    }
}
```
- No.122 买卖股票的最佳时机Ⅱ **动态规划**  
和上一题的区别是 交易次数不限
```
class Solution {
    public int maxProfit(int[] prices) {
        int len=prices.length;
        int[][] dp=new int[len][2];
        if(len==0)return 0;
        dp[0][0]=0;
        dp[0][1]=-prices[0];
        for(int i=1;i<len;i++){
            dp[i][0]=Math.max(dp[i-1][0],dp[i-1][1]+prices[i]);
            dp[i][1]=Math.max(dp[i-1][0]-prices[i],dp[i-1][1]);
        }
        return dp[len-1][0];
    }
}
```
- No.123 买卖股票的最佳时机 III **困难**
- No.124 二叉树中的最大路径和 **困难**
- No.125 验证回文串
```
class Solution {
    public boolean isPalindrome(String s) {
        HashMap<Character,Integer> map=new HashMap();
        for(int i=0;i<=9;i++){
            map.put((char)('0'+i),i);
        }
        for(int i=0;i<26;i++){
            map.put((char)(97+i),10+i);
            map.put((char)('A'+i),10+i);
        }
        int len=s.length();
        int front=0;
        int end=len-1;
        while(front<end){
            while(front<len&&map.get(s.charAt(front))==null){
                front++;
            }
            while(end>-1&&map.get(s.charAt(end))==null){
                end--;
            }
            if(front<end){
                if(map.get(s.charAt(front))!=map.get(s.charAt(end)))return false;
                else{
                    front++;
                    end--;
                }
            }
        }
        return true;
    }
}
```
