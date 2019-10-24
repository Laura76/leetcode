No.151 翻转字符串里的单词  **栈**
```
class Solution {
    public String reverseWords(String s) {
        Stack<String> stack=new Stack<String>();
        StringBuilder builder=new StringBuilder();
        for(int i=0;i<s.length();i++){
            while(i<s.length()&&s.charAt(i)==' ')i++;
            int start=i;i++;
            while(i<s.length()&&s.charAt(i)!=' ')i++;
            if(start<s.length())stack.push(s.substring(start,i));
        }
        while(!stack.isEmpty()){
            builder.append(stack.pop());
            builder.append(" ");
        }
        if(builder.length()>0)builder.deleteCharAt(builder.length()-1);
        return builder.toString();
    }
}
```
No.152 乘积最大子序列  **dp**
要大胆地dp
```
class Solution {
    public int maxProduct(int[] nums) {
        int len=nums.length;
        if(len==0)return 0;
        int res=nums[0];
        int pre_max=nums[0];int pre_min=nums[0];
        for(int i=1;i<len;i++){
            int temp=pre_max;
            pre_max=Math.max(Math.max(pre_max*nums[i],nums[i]),pre_min*nums[i]);
            pre_min=Math.min(Math.min(temp*nums[i],nums[i]),pre_min*nums[i]);
            res=Math.max(res,pre_max);
        }
        return res;
    }
}
```
No.153 寻找旋转排序数组中的最小值
