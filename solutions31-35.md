- 第三十一题 下一个排列
```
class Solution {
    public void nextPermutation(int[] nums) {
        int len=nums.length;
        int i=len-1;
        for(;i>=1;i--){
            if(nums[i]>nums[i-1]){
                break;
            }
        }
        //已经是最大序列了即倒序序列
        if(i==0){
            reverse(nums);
            return;
        }
        for(int j=len-1;j>=i;j--){
            if(nums[j]>nums[i-1]){
                int temp=nums[i-1];
                nums[i-1]=nums[j];
                nums[j]=temp;
                break;
            }
        }        
        //倒置i后面的元素
        for(int j=i;j<(i+(len-i)/2);j++){
            int temp=nums[j];
            nums[j]=nums[i+len-1-j];
            nums[i+len-1-j]=temp;
        }
    }
    public void reverse(int[] nums){
        int len=nums.length;
        for(int i=0;i<len/2;i++){
            int temp=nums[i];
            nums[i]=nums[len-1-i];
            nums[len-1-i]=temp;
        }
    }
}
```