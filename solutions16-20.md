- 第十六题 最接近的三数之和
```
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int len=nums.length;
        int sum=0;
        int res=nums[0]+nums[1]+nums[len-1];
        for(int i=0;i<len;i++){
            int left=i+1;
            int right=len-1;
            while(left<right){
                sum=nums[i]+nums[left]+nums[right];
                if(sum==target)return target;
                else if(sum<target){
                    left++;
                }else if(sum>target){
                    right--;
                }
                res=Math.abs(res-target)>Math.abs(sum-target)?sum:res;
            }
        }
        return res;
    }
}
```
- 第十七题 电话号码的字母组合
```
class Solution {
    Map<String,String> map=new HashMap<String,String>(){
        {
            put("2","abc");
            put("3","def");
            put("4","ghi");
            put("5","jkl");
            put("6","mno");
            put("7","pqrs");
            put("8","tuv");
            put("9","wxyz");
        }
    };
    List<String> res=new LinkedList<String>();
    public void letterCombiCore(String curr,String digitsLeft){
        if(digitsLeft.equals("")){
            res.add(curr);
            return;
        }else{
            String digit=digitsLeft.substring(0,1);
            String equiva=map.get(digit);
            for(int i=0;i<equiva.length();i++){
                letterCombiCore(curr+equiva.substring(i,i+1),digitsLeft.substring(1));
            }
        }
    }
    public List<String> letterCombinations(String digits) {
        if(digits.equals(""))return res;
        letterCombiCore("",digits);
        return res;
    }
}
```
- 第十八题 四数之和
```
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        int len=nums.length;
        int sum=0;
        List<List<Integer>> res=new LinkedList<>();
        for(int i=0;i<=len-4;i++){
            if(i>0&&nums[i]==nums[i-1])continue;
            for(int j=i+1;j<=len-3;j++){
                if(j>i+1&&nums[j]==nums[j-1])continue;
                int left=j+1;
                int right=len-1;
                while(left<right){
                    sum=nums[i]+nums[j]+nums[left]+nums[right];
                    if(sum==target){
                        res.add(Arrays.asList(nums[i],nums[j],nums[left],nums[right]));
                        left++;right--;
                        while(left<len&&nums[left]==nums[left-1]){
                            left++;
                        }
                        while(right>-1&&nums[right]==nums[right+1]){
                            right--;
                        }
                    }else if(sum<target){
                        left++;
                        while(left<len&&nums[left]==nums[left-1]){
                            left++;
                        }
                    }else if(sum>target){
                        right--;
                        while(right>-1&&nums[right]==nums[right+1]){
                            right--;
                        }
                    }
                }
            }
        }
        return res;
    }
}
```
