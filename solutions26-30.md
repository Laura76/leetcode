- 第二十六题 删除排序数组中重复项
```
class Solution {
    public int removeDuplicates(int[] nums) {
        int len=nums.length;
        int i=0;
        for(int j=1;j<len;j++){
            if(nums[j]!=nums[i]){
                i++;
                nums[i]=nums[j];
            }
        }
        return i+1;
    }
}
```
